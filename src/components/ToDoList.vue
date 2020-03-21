<template>
<div>
<input type="text"
class="todolist"
placeholder="what needs to be done"
v-model="newTodo"
@keyup.enter="addToDo()">
  <div v-for="(todo,index) in todos" :key="todo.id"
        class="todoitem" v-model="newTodo" >
     <div>
     <div v-if="!todo.editing" @dblclick="editTodo(todo)">
      {{ todo.title }}
      </div>
      <input v-else type="text" v-model="todo.title" @blur="doneEdit(todo)" 
      @keyup.enter="doneEdit(todo)" v-focus> 
      </div>
  <div class="remove-item" @click="removeToDo(index)">
  &times;
  </div>
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
          'editing' : false,
        },
        {
          'id' : 2,
          'title' : 'Finish Vue 2',
          'completed' : false,
          'editing' : false,
        },
      ]
    } 
  },
  directives :{
    focus:{
      inserted: function(e1){
        e1.focus()
      }
    }
  },
  methods : {
    addToDo()
    {
        if(this.newTodo.trim().length ==0){
          return
        }
        this.todos.push({
          id: this.idForToDo,
          title:this.newTodo,
          completed:false,
        })
        this.newTodo =''
        this.idForToDo++
    },
    editTodo(todo){
      todo.editing = true
    },
    doneEdit(todo){
      todo.editing = false
    },
    removeToDo(index)
    {
      this.todos.splice(index,1);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.todolist{
  width:100%;
}
.todoitem{
  display : flex;
  align-items : center;
  justify-content: space-between;
  font-weight:bold;
  margin: 20px auto;
  
}
.remove-item{
  cursor: pointer;
}
</style>
