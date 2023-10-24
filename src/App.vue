<template>
  <div class="app">
    <div class="todo-wrap">
        <TodoHeader @createTodo="createTodo"></TodoHeader>
        <TodoMain @makeSuccess="makeSuccess" @deleteTodo="deleteTodo" :todos="sortByAny"></TodoMain>
    </div>
    <Sort v-model:currentSort="currentSort"></Sort>
  </div>

</template>

<script>
import TodoHeader from '@/components/TodoHeader.vue'
import TodoMain from '@/components/TodoMain.vue'
import Sort from '@/components/Sort.vue'
export default {
  components: { TodoHeader, TodoMain, Sort },
  data() {
    return {
      todos: JSON.parse(localStorage.getItem('todos')) || [],
      sortedTodos: [],
      currentSort: ''
    }
  },
  methods: {
    createTodo(todo) {
      const td = {
        body: todo,
        isActive: false,
        id: crypto.randomUUID()
      }
      this.todos.push(td)
      localStorage.setItem('todos', JSON.stringify(this.todos))
    },
    deleteTodo(todo) {
     this.todos = this.todos.filter(td => td.id !== todo.id)
     localStorage.setItem('todos', JSON.stringify(this.todos))
    },
    makeSuccess(todo) {
      todo.isActive ? todo.isActive = false : todo.isActive = true
      
      localStorage.setItem('todos', JSON.stringify(this.todos))
    },
  },
  computed: {
    sortByAny() {
      switch (this.currentSort) {
        case 'succ':
          return this.sortedTodos = this.todos.filter(td => td.isActive)
        case 'all': 
          return this.todos
        case 'unsucc': 
          return this.sortedTodos = this.todos.filter(td => !td.isActive)
        default: 
          return this.todos
      }
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family:Verdana, Geneva, Tahoma, sans-serif
  
}


::-webkit-scrollbar{
  outline: none;
}

@media (max-width: 970px){
  div.todo-wrap {
    margin-top: auto;
    width: auto;
    border: none;
    height: 600px;
    
  }

  div.sort {
   position: static;
   bottom: 5%;
   justify-content: center !important;
   flex-direction: row;
   grid-gap: 50px !important;
   width: 400px !important;
   
  }

  #succ {
    width: 400px !important;
  }
  #all {  
    width: 400px !important;
  }
  #unsucc {
    width: 400px !important;
  }
}

@media (max-width: 420px) {
  div.sort {
    width: 250px !important;
    grid-gap: 25px !important;
  }
  #succ {
    width: 25px !important;
   
  }
  #all {
    width: 25px !important;
  }
  #unsucc {
    width: 25px !important;
  }

  .big-suc {
    display: none !important;
  }
  .small-suc{
    display: block !important;
  }

  .big-unsuc {
    display: none !important;
  }
  .small-unsuc{
    display: block !important;
  }
  
}

@media (max-width: 320px) {
  textarea {
    min-width: 25px !important;
  }
  
}

@media (max-height: 650px) {
    .todo-wrap {
      height: 85vh !important;
    }
}


body {
  background-color:honeydew;
}


textarea {
  min-height: 50px;
  min-width: 225px;
  max-height: 410px;
  padding: 15px 20px;
  outline: none;
  resize: none;
   
}

.todo-wrap {
  box-shadow: 5px 5px 5px #999;
  overflow: hidden;
  overflow-y: scroll;
  margin-top: 20px;
  margin-left: auto;
  margin-right: auto;
  width: 900px;
  border: 3px solid darkslategrey;
  border-radius: 15px;
  height: 800px;
  background-color:aliceblue;
}





</style>