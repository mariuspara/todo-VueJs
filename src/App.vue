<template>
<div>
  <appNewTodoElement @todoAdded="newTodoElement" @todoDeleted="deleteTodo" />
  <!-- <div class="priority-filters">
    <div>Filters:</div>
    High: <input type="checkbox" id="checkbox" v-model="checkedHigh">
    Medium: <input type="checkbox" id="checkbox" v-model="checkedMedium">
    Low: <input type="checkbox" id="checkbox" v-model="checkedLow">
  </div> -->

  <todoMain :todos="todos"/>
</div>
  
</template>

<script>
import todoMain from './components/todoMain.vue';
import newTodoElement from './components/newTodoElement'

export default {

  data () {
    return {
      todos: [{
        title: '',
        Priority: 'low',
        done: false
      }]
    }
  },
  mounted() {
    if (localStorage.getItem('todos')) this.todos = JSON.parse(localStorage.getItem('todos'));
  },
  watch: {
    todos: {
      handler() {
        localStorage.setItem('todos', JSON.stringify(this.todos));
    },
  },
},
  methods: {
    newTodoElement(todo){
      this.todos.push(todo);
      localStorage.setItem('todos', JSON.stringify(this.todos));
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
    }
  },
    components: {
    todoMain,
    appNewTodoElement: newTodoElement
  },
  
}
</script>

<style lang="css">
  input {
    width: 100%;
    height: 50px;
    border: 1px solid #ccc;
    border-radius:5px;
    padding-left:20px
  }
  select {
    height: 50px;
    padding-left:10px;
    border: 1px solid #ccc;
    border-radius:5px;
  }
  .priority-filters {
    display: flex;
    align-items: center;

}
</style>
