<template>
    <li @mouseenter="handleEnter(true)" @mouseleave="handleEnter(false)" :style="{background: bgColor}">
      <label>
        <input type="checkbox" v-model="todo.complete">
        <span>{{todo.title}}</span>
      </label>
      <button v-show="isShow"  @click="deleteItem">删除</button>
    </li>
</template>

<script>
  import PubSub from 'pubsub-js'
  export default {
    name: 'ToDoItem',
    props: {
      todo: Object,
      index: Number,

    },
    data() {
      return {
        bgColor: 'white', // 默认的背景颜色
        isShow: false //默认是否显示
      }
    },
    methods: {
      handleEnter(isEnter) {
        if(isEnter) {
          this.bgColor = 'gray'
          this.isShow = true
        } else {
          this.bgColor = 'white'
          this.isShow = false
        }
      },
      deleteItem () {
        const {todo, index, deleteTodo} = this;
        if( window.confirm(`确认删除${todo.title}吗？`) ){
          //deleteTodo(index)
          // 发布消息
          PubSub.publish('deleteTodo', index)
        }
      }
    }
  }
</script>

<style scoped>
  li {
    list-style: none;
  }
  label {
    width: 150px;
    display: inline-block;
  }

</style>
