<template>
  <div>
    <input type="text" placeholder="请输入你的任务名称，按回车键确认" v-model="title" @keyup.enter="addItem">
  </div>
</template>

<script>
  export default {
    name: 'ToDoHeader',
    props: {

    },
    data() {
      return {
        title: '',

      }
    },
    methods: {
      addItem(){
        // 1. 检查输入的合法性
        const title = this.title.trim();
        if(!title ){
          alert("必须输入");
          return;
        }
        //2. 根据输入生成一个todo对象
        const todo = {
          title,
          complete: false
        }
        // 3. 添加到todos
        //this.addTodo(todo);
        // 触发自定义事件：addTodo
        this.$emit('addTodo', todo)

        // 4. 清除输入
        this.title='';
      }
    }
  }
</script>

<style scoped>
  input {
    width: 300px;
  }
</style>
