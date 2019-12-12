<template>
  <div>
    <ToDoHeader :addTodo="addTodo"/>
    <ToDoList :todos="todos" :deleteTodo="deleteTodo" />
    <ToDoFooter :todos="todos" :deteleCompleteTodos="deteleCompleteTodos" :seleteAllTodos="seleteAllTodos"/>
  </div>
</template>

<script>
  import ToDoHeader from './components/ToDoHeader'
  import ToDoList from './components/ToDoList'
  import ToDoFooter from './components/ToDoFooter'

  export default {
    name: 'App',
    data () {
      return {
        // 从localStorage 读取todos
        todos: JSON.parse(window.localStorage.getItem('todos_key') || '[]' )
        //   [
        //   {title: '吃饭', complete: false},
        //   {title: '睡觉', complete: true},
        //   {title: 'coding', complete: false},
        //   {title: '打游戏', complete: false},
        // ]
      }
    },
    methods: {
      addTodo(todo) {
        this.todos.unshift(todo)
      },
      deleteTodo (index) {
        this.todos.splice(index, 1)
      },
      // 删除所有选中的todo
      deteleCompleteTodos () {
        // 过滤 留下complete为false的
        this.todos = this.todos.filter(todo => !todo.complete)
      },
      // 全选，全不选
      seleteAllTodos (check){
        this.todos.map(todo => todo.complete = check )
      }
    },
    watch: { // 深度监视
      todos: {
        deep: true, // 深度监视
        handler: function(value){
          // 将 todos 最新的值的json数据，保存到localStorge中
          window.localStorage.setItem('todos_key', JSON.stringify(value))
        }
      }

    },
    components: {
      ToDoHeader,
      ToDoList,
      ToDoFooter
    }
  }
</script>

<style scoped>

</style>
