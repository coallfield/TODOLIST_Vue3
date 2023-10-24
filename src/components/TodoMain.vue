<template>
  <div class="todos-wrapper">
    <TransitionGroup name="todo-list">
      <div v-for="todo in todos" :key="todo.id" class="todos">
        <textarea @click="setHeight" wrap="hard" readonly :class="{ 'active': todo.isActive }"
          class="td todo-text">{{ todo.body }}</textarea>
        <div class="btns">
          <button 
              @mouseover="$event.target.classList.add('suc-btn-over')"
              @mouseout="$event.target.classList.remove('suc-btn-over')"              
              :class="{ 'suc-btn': todo.isActive}" 
              @click="makeSuccess(todo)" 
              id="success">✓️</button>             
          <button 
                  @mouseover="$event.target.classList.add('delete-active')"
                  @mouseout="$event.target.classList.remove('delete-active')" 
                  @click="deleteTodo(todo)" 
                  id="delete">✖</button>
        </div>
      </div>
    </TransitionGroup>
    
  </div>
</template>

<script>

export default {
  props: {
    todos: {
      type: Array,
      required: true
    }
  },
  methods: {
    makeSuccess(todo) {
      this.$emit('makeSuccess', todo)

    },
    deleteTodo(todo) {
      this.$emit('deleteTodo', todo)
    },
    setHeight(event) {
        if( event.target.style.height ===  `${event.target.scrollHeight}px`){
          event.target.style.height = '50px'
        } else {
          event.target.style.height = `${event.target.scrollHeight}px`
        }
    }
  }
  
}
</script>

<style scoped>
.todos-wrapper {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;

}

.todos {
  
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: flex-start;
  grid-gap: 10px
}



.td {
  box-shadow: 5px 5px 5px #999;
  overflow: hidden;
  overflow-y: scroll;
  word-break: keep-all;
  margin-left: 10px;
  margin-top: 30px;
  width: 80%;
  height: 50px;
  border-radius: 20px;
  border: 2px solid darkslategrey;
  background-color: white;
}

.btns {
  display: flex;
  align-items: center;
}

#success {
  margin-top: 17px;

  font-size: 2.5rem;
  outline: none;
  background: none;
  border: none;

}

#delete {

  margin-top: 20px;
  margin-left: 5px;
  font-size: 2rem;
  outline: none;
  background: none;
  border: none;
}


.suc-btn {
  color: green;
}

.suc-btn-over {
  color: green;
}

.delete-active {
  color: red;
}


.active {
  opacity: 25%;
  border: 2px solid green;
  background: green;
  color: white;
  resize: none
}




.todo-list-move,
.todo-list-enter-active,
.todo-list-leave-active {
  transition: all 0.5s ease;
}

.todo-list-enter-from,
.todo-list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
.todo-list-leave-active {
  position: absolute;
  width:100%;
  
}
</style>