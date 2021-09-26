<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <br />
    <HelloWorld :msg="msg" :is-show="show" />
    <Calculator/>
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue'
import HelloWorld from './components/HelloWorld.vue'
export default {
  name: 'App',
  components: {
    HelloWorld,
    Calculator
  },
  data: () => ({
    show: true,
    msg: 'Welcome to Your Vue.js App'
  })
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
