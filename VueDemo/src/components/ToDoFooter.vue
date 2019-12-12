<template>
  <div>
<!--    <input type="checkbox" v-model="isAllCheck">-->
    <slot name="checkAll"></slot>
<!--    <span>已完成{{completeSize}}  /  全部{{todos.length}}</span>-->
    <slot name="count"></slot>
<!--    <button v-show="completeSize" @click="deteleCompleteTodos">清除已完成任务</button>-->
    <slot name="delete"></slot>
  </div>
</template>

<script>
  export default {
    name: 'ToDoFooter',
  }
</script>

<style scoped>

</style>
