<template>
  <div id="app">
    <MyCards></MyCards>
  </div>
</template>

<script>
import MyCards from './components/MyCards'

export default {
  name: 'App',
  components: {
    MyCards
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
