<template>
    <div class="container">
      <div class="filter-todo">
      <div>Filters:</div>
      <div class="filter-elements">
        <label for="allTodo">All: </label>
        <input type="checkbox" name="all" id="allTodo" v-model="allTodo">
        <label for="highTodo">High: </label>
        <input type="checkbox" name="high" id="highTodo" v-model="highTodo">
        <label for="mediumTodo">medium: </label>
        <input type="checkbox" name="medium" id="mediumTodo" v-model="mediumTodo">
        <label for="lowTodo">low: </label>
        <input type="checkbox" name="low" id="lowTodo" v-model="lowTodo">
      </div>
    </div>
      <todo-element 
      v-for="(todo, index) in filtredTodos" 
      :key="index"
      @delete-todo="deleteTodo" 
      v-bind:todo="todo" 
      v-on:complete-todo="completeTodo(index)" 
      >{{todo}}</todo-element>
</div> 
    
</template>

<script>
import todoElement from './todoElement.vue'

export default {

    props: ['todos'],
    data(){
      return {
        highTodo:false,
        mediumTodo:false,
        lowTodo:false,
        allTodo:true
      }
      
    },
    components: {
      todoElement: todoElement
    },
    methods: {
      deleteTodo(todo) {
        const todoIndex = this.todos.indexOf(todo);
        this.todos.splice(todoIndex, 1);
      },
      completeTodo(index) {
      this.todos[index].done = true;
      localStorage.setItem('todos', JSON.stringify(this.todos));
      },
    },
      computed :{
        filtredTodos(){
          let filtredTodosArray = [];
         filtredTodosArray = this.todos.filter(item => {
           if(this.allTodo === true) {
             return true;
           }
           else if(this.highTodo === true && item.Priority === "High") {
             return true;
           }
           else if(this.mediumTodo === true && item.Priority === "Medium") {
             return true
           }
           else if(this.lowTodo === true && item.Priority === "Low") {
             return true;
           }
         })

         return filtredTodosArray;
    }
  }
    }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.filter-todo {
  display: flex;
  align-items: center;
}
.filter-elements {
  display: inline-flex;
  align-items: center;
}

label,input{
  margin: 10px;
}

</style>
