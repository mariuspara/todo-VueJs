<template>
    <div class="container">
        <h1>Todo app</h1>
        <div class="commands">
          <input v-model="todo.title" type="text">
          <button @click.prevent="createNew">+</button>
        </div>
        <div class="priority">
            <div>Priority:</div>
            <select v-model="picked">
                <option disabled value="">Please select one</option>
                <option>High</option>
                <option>Medium</option>
                <option>Low</option>
            </select>
        </div>

        


    </div>
</template>

<script>
    export default {
        data() {
            return {
                picked:null,
                todo:{
                    title: '',
                    Priority: '',
                    done:false
                },
            }
        },
        methods: {
            createNew(){
                this.todo.Priority = this.picked;
                this.$emit('todoAdded', this.todo);
                this.picked = null;
                this.todo = {
                    title: '',
                    Priority: '',
                    done:false
                };
            }
        }
    }
</script>

<style scoped>
    input {
        width: 100%;
        height: 50px;
        border: 1px solid #ccc;
}
.container {
  max-width: 768px;
  margin: 0 auto;
}

.commands {
  display: flex;
  align-items: center;
}

.commands button {
  background-color: cornflowerblue;
  width: 30px;
  height: 30px;
  margin: 5px;
  border:1px dotted #ccc;
}
.priority {
    display: flex;
    align-items: center;
    margin-top:50px;
}
.priority label {
    margin:5px;
}

</style>