<template>
    <div class="todoz">
        <div v-if="!editing">
            <span class='text' @click="enableEditing">{{todo.title}}</span>
        </div>
        <div v-if="editing">
          <input v-model="tempValue" class="input"/>
          <button @click="disableEditing"> Cancel </button>
          <button @click="saveEdit"> Save </button>
        </div>
        <div>{{todo.Priority}}</div>
        <div>
            <button v-on:click="completeTodo(todo)">Complete</button>
            <button v-on:click="deleteTodo(todo)">Remove</button>
            <div class="ui bottom attached green basic button" v-show="!editing && todo.done" disabled>
        Completed
    </div>
    <div class="ui bottom attached red basic button" v-show="!editing && !todo.done" v-on:click="completeTodo(todo)">
        Pending
    </div>
        </div>
        
    </div>
</template>

<script>
export default {
  props: ["todo"],
  data(){
      return {
        isComplete:false,
        tempValue: null,
        editing: false
      }
  },
  methods:{
    deleteTodo(todo) {
      this.$emit("delete-todo", todo);
    },
    completeTodo(todo) {
      this.$emit("complete-todo", todo);
    },
    enableEditing: function(){
      this.tempValue = this.todo.title;
      this.editing = true;
    },
    disableEditing: function(){
      this.tempValue = null;
      this.editing = false;
    },
    saveEdit: function(){
      // However we want to save it to the database
      this.todo.title = this.tempValue;
      this.disableEditing();
    }
  }
}
</script>

<style scoped>
    .todoz {
        border:1px solid #ccc;
        border-radius:10px;
        margin: 20px 0;
        padding: 20px;
        display: flex;
        justify-content: space-between;
    }
    button {
        padding: 5px;
        border:1px solid black;
        margin:10px;
        border-radius: 5px;
    }
</style>