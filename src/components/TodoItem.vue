<template>
<li>
  <div>
    <label><input v-if="todo.isCompleted" class="checkbox" type="checkbox" checked @click="toggleChecked">
    <input v-else class="checkbox"  type="checkbox" @click="toggleChecked">
    {{todo.caption}}</label>
  </div>
  <button
  @click="deleteTodo">x</button>
</li>
</template>
<script>

export default {
  name: 'todo-item',
  props: ['todo'],
  methods: {
    deleteTodo(){
      //deleting a todo item
      this.$emit('deleteTodo', this.todo);
    },
    toggleChecked(){
      //toggling check box
      this.$emit('toggleChecked', this.todo);
    },
  },
}
</script>
<style scoped>
 div{
   display: flex;
   flex-direction: row;
 }
 p{
   margin: 0;
 }
 li{
   display: flex;
   justify-content: space-between;
   list-style: none;
   width: 50%;
 }
 .checkbox:hover{
    cursor: pointer;
 }
</style>
