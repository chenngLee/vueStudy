<template>
  <div>
    <input type="checkbox" v-model="isAllCheck">
    <span>已完成{{completeSize}}  /  全部{{todos.length}}</span>
    <button v-show="completeSize" @click="deteleCompleteTodos">清除已完成任务</button>
  </div>
</template>

<script>
  export default {
    name: 'ToDoFooter',
    props: {
      todos: Array,
      deteleCompleteTodos: Function,
      seleteAllTodos: Function
    },
    computed: {
      completeSize () {
        return this.todos.reduce((preTotal, todo) => preTotal + (todo.complete?1:0), 0)
      },
      isAllCheck: {
        get () {
          return this.completeSize === this.todos.length && this.completeSize > 0
        },
        set ( value ) { // value 是当前checkbox的最新值
          this.seleteAllTodos(value)
        }
      }
    }

  }
</script>

<style scoped>

</style>
