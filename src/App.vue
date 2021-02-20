<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/peiko-logo-mini.png">
    <h1>Test</h1>
    <hr>
    <div class="container">
      <data-currency></data-currency>
    </div>
  </div>
</template>

<script>
import DataCurrency from "@/components/DataCurrency";

export default {
  name: 'App',
  components: {
    DataCurrency
  },
}
</script>

<style lang="sass">
body
  font-size: 16px

#app
  font-family: Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  text-align: center
  color: #2c3e50
  margin-top: 60px


.container
  width: fit-content
  margin: 2rem auto
  padding: 2rem
  border: 1px solid #d7d7d7

</style>
