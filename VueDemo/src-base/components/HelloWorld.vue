<template>
    <div>
      <p class="msg">{{msg}}</p>
    </div>
</template>

<script>
  export default {
    name: 'HelloWorld',
    data () { // 必须写函数
      return {
        msg: 'Hello Vue Component'
      }
    }
  }
</script>

<style scoped>
  .msg{
    color: red;
    font-size: 30px;
  }
</style>
