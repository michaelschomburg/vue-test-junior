<template>
  <div id="app">
    <calculator v-on:get-quote="showQuote"></calculator>
    <quote :displayQuote="quote"></quote>
  </div>
</template>

<script>
import calculator from './components/calculator.vue'
import quote from './components/quote.vue'
import axios from 'axios'
export default {
  components: {
    calculator,quote
  },
  data() {
    return {
      errors: '',
      quote: '',
    }
  },
  methods: {
    showQuote() {
      axios.get('https://api.kanye.rest')
              .then(response => {
                this.quote = response.data.quote
              })
              .catch(e => {
                this.errors.push(e)
              })
    }
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
