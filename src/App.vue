<template>
  <div id="app">
    <calculator msg="Welcome to Your Vue.js App"/>
    <quote></quote>
  </div>
</template>

<script>
import calculator from './components/calculator.vue'
import quote from './components/quote.vue'
export default {
  name: 'app',
  components: {
    calculator,quote
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
