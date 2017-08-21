<template>
  <section>
    <h1>Hello world!</h1>
    <ul>
      <todo-item
      v-for="todo in todoItems" 
      :key="todo.caption"
      :todo="todo"
      @deleteTodo="deleteTodo"
      @toggleChecked="toggleChecked"
      class="item"
      ></todo-item>
    </ul>
    <todo-input
    @todoAdded="addTodo"
    ></todo-input>
  </section>
</template>
<script>
import TodoItem from './TodoItem'
import TodoInput from './TodoInput'
export default {
  name: 'todo',
  data(){
    return{
      todoItems: [{caption:'todo', isCompleted:true}]
    }
  },
   components: {
    TodoItem,
    TodoInput
  },
  created(){
    let newTodoItems = JSON.parse(localStorage.getItem('todos'));
    if(newTodoItems)
      this.todoItems = newTodoItems;
  },
  methods: {
    addTodo(value){
      this.todoItems.push(this.createNewTodo(value));
      localStorage.setItem('todos',JSON.stringify(this.todoItems));
    },
    createNewTodo(caption){
      return { caption, isCompleted:false }
    },
    deleteTodo(todo){
      let idx = this.todoItems.findIndex( todoItem => todoItem === todo );
      this.todoItems.splice(idx);
      localStorage.setItem('todos',JSON.stringify(this.todoItems));
    },
    toggleChecked(todo){
      let idx = this.todoItems.findIndex( todoItem => todoItem === todo );
      this.todoItems[idx].isCompleted = !this.todoItems[idx].isCompleted;
      localStorage.setItem('todos',JSON.stringify(this.todoItems));
    },
  }
}
</script>
<style>
  .item{
    transition: 0.5s;
    border-radius: 10%;
  }
  .item:hover{
    background-color: rgba(128,128,128,0.5)
  }
  ul{
    display: flex;
    align-content: center;
    flex-direction: column;
  }
  li{
    align-self: center;
  }
  button:hover{
    cursor: pointer;
  }
</style>
