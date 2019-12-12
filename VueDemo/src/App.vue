<template>
  <div>
<!--    <ToDoHeader @addTodo="addTodo"/> &lt;!&ndash; 给ToDoHeader标签对象绑定 addTodo 事件监听 &ndash;&gt;-->
    <ToDoHeader ref="header" />
    <ToDoList :todos="todos"  />
<!--    <ToDoFooter :todos="todos" :deteleCompleteTodos="deteleCompleteTodos" :seleteAllTodos="seleteAllTodos"/>-->

    <ToDoFooter>
      <input type="checkbox" v-model="isAllCheck" slot="checkAll">
      <span slot="count">已完成{{completeSize}}  /  全部{{todos.length}}</span>
      <button v-show="completeSize" @click="deteleCompleteTodos" slot="delete">清除已完成任务</button>
    </ToDoFooter>

  </div>
</template>

<script>
  import PubSub from 'pubsub-js'
  import ToDoHeader from './components/ToDoHeader'
  import ToDoList from './components/ToDoList'
  import ToDoFooter from './components/ToDoFooter'

  import storageUtil from './util/storageUtil'

  export default {
    name: 'App',
    data () {
      return {
        // 从localStorage 读取todos
        todos: storageUtil.readTodos()
      }
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
    },
    mounted () { // 执行一些异步代码
      // 给 <ToDoHeader /> 绑定addTodo事件监听
      // this.$on('addTodo', this.addTodo)
      this.$refs.header.$on('addTodo', this.addTodo)

      // 订阅消息
      PubSub.subscribe('deleteTodo', (msg, index) => {
        console.log(msg, index);
        this.deleteTodo(index)
      })
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
        //过滤 留下complete为false的
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
        // handler: function(value){
        //   // 将 todos 最新的值的json数据，保存到localStorge中
        //   storageUtil.saveTodos(value)
        // }
        handler: storageUtil.saveTodos
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
