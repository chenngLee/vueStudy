<template>
<div id="app">
    <p>click {{count}} times, count is {{evenOrOdd}}</p>
    <button @click="increment">+</button>
    <button @click="decrement">-</button>
    <button @click="incrementIfOdd">increment if odd</button>
    <button @click="incrementAsync">increment async</button>
  </div>
</template>

<script>
import {mapState, mapGetters, mapActions} from 'vuex'
export default {
  name: 'app',
  computed: {
    ...mapState(['count']), //mapState() 返回值：{count(){return this.$store.state['count']}}
    ...mapGetters(['evenOrOdd']),//mapGetters() 返回值：{evenOrOdd(){return this.$store.getters['evenOrOdd']}}

    // evenOrOdd () {
    //   return this.$store.getters.evenOrOdd
    // },
    // count () {
    //   return this.$store.state.count
    // }
  },
  methods: {
    ...mapActions(['increment', 'decrement', 'incrementIfOdd', 'incrementAsync'])
  }
  // methods: {
  //   increment () {
  //     // 通知vuex去增加
  //     this.$store.dispatch('increment') // 触发store中对应的action调用
  //   },
  //   decrement () {
  //     this.$store.dispatch('decrement')
  //   },
  //   incrementIfOdd () {
  //     this.$store.dispatch('incrementIfOdd')
  //   },
  //   incrementAsync () {
  //     this.$store.dispatch('incrementAsync')
  //   },
  // }
}
</script>

<style>

</style>
