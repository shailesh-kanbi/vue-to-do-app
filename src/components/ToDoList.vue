<template>
<div>
<input type="text"
class="todolist"
placeholder="what needs to be done"
v-model="newTodo"
@keyup.enter="addToDo()">
  <div v-for="todo in todos" :key="todo.id"
        class="todo-item" v-model="newTodo" >
  {{ todo.title }}
  </div>
  </div>
</template>

<script>
export default {
  name: 'ToDoList',
  data () {
    return {
      newTodo: '',
      idForToDo: 3,
      todos :[
        {
          'id' : 1,
          'title' : 'Finish Vue',
          'completed' : false,
        },
        {
          'id' : 2,
          'title' : 'Finish Vue 2',
          'completed' : false,
        },
      ]
    } 
  },
  methods : {
    addToDo()
    {
        this.todos.push({
          id: this.idForToDo,
          title:this.newTodo,
          completed:false,
        })
        this.newTodo =''
        this.idForToDo++
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.todolist{
  width:100%;
}
</style>
