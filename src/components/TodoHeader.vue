<template>
     <div class="todo">
          <div class="main-todo">
            <h1 class="title">TODO LIST</h1>
            <input placeholder="Type something..." @input="todoBody = $event.target.value" :value="todoBody" class="todo-body">
            <SortButton
                  style="background-color: honeydew; width: 25%;"
                  @mouseover="$event.target.classList.add('confirm-active')" 
                  @mouseout="$event.target.classList.remove('confirm-active')" 
                  @click="createTodo" 
                  >Confirm</SortButton>
            <div v-if="showAttention" class="attention">Сome up with a task</div>
          </div>
        </div>

</template>

<script>

export default {
    data() {
        return {
            todoBody: '',
            showAttention: false
        }
    },
    methods: {
        createTodo(event) {
          
            event.target.classList.add('confirm-active')
            setTimeout(() => {
              event.target.classList.remove('confirm-active')
            }, 100)

            if (!this.todoBody.trim()) {
                this.showAttention = true
                setTimeout(() => {
                    this.showAttention = false
                }, 1000)
                return
            }
            
            this.showAttention = false
            this.$emit('createTodo', this.todoBody)
            this.todoBody = ''

        }
    },
    
}
</script>


<style scoped>
.main-todo {
  display: flex;
  padding: 5px;
  grid-gap: 10px;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  position: relative;
}

.title {
  color:darkslategrey;
  
  
}

.todo-body {
  box-shadow: 5px 5px 5px #999;
  width: 50%;
  height: 50px;
  border-radius: 10px;
  border: 2px solid darkslategrey;
  padding-left: 5px;
  outline: none;
}

.attention {
    color: red;
    position: absolute;
    top:100%
}
</style>