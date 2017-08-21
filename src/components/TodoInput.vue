<template>
    <section>
        <input v-model="inputText" type="text">
        <button @click="addTodoItem">Add</button>
    </section>
</template>
<script>
export default {
    name:'todo-input',
    data(){
        return {
            inputText:'',
        }
    },
    methods: {
        addTodoItem(){
            //adding a todo item
            this.$emit('todoAdded', this.inputText);
        },
    }
}
</script>
<style>

</style>
