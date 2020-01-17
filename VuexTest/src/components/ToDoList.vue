<template>
  <ul>
    <ToDoItem v-for="(todo, index) in todos" :key="index" :todo="todo" :index="index" :deleteTodo="deleteTodo" />
  </ul>
</template>

<script>
  import ToDoItem from './ToDoItem'

  export default {
    name: 'ToDoList',
    props: {
      todos: Array,
      deleteTodo: Function
    },
    components: {
      ToDoItem
    }
  }
</script>

<style scoped>

</style>
