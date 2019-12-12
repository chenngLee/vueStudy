<template>
  <ul>
    <ToDoItem v-for="(todo, index) in todos" :todo="todo" :index="index" />
  </ul>
</template>

<script>
  import ToDoItem from './ToDoItem'

  export default {
    name: 'ToDoList',
    props: {
      todos: Array,

    },
    components: {
      ToDoItem
    }
  }
</script>

<style scoped>

</style>
