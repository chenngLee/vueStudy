<template>
  <div>
    <input type="text" placeholder="请输入你的任务名称，按回车键确认" v-model="title" @keyup.enter="addItem">
  </div>
</template>

<script>
  export default {
    name: 'ToDoHeader',
    props: {
      addTodo: Function
    },
    data() {
      return {
        title: '',

      }
    },
    methods: {
      addItem(){
        const title = this.title.trim();
        if(!title ){
          alert("必须输入");
          return;
        }
        const todo = {
          title,
          complete: false
        }
        this.addTodo(todo);
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
