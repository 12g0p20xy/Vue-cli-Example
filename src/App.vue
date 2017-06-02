<template>
  <div id="app">
    <count></count>
    <signup></signup>
  </div>
</template>

<script>
import Count from './components/Count'
import Signup from './components/Signup'

export default {
  name: 'app',
  components: {
    Count,
    Signup
  }
}
</script>

<style>
@import 'https://cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap.min.css';
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 30px;
}
.count{
  margin-bottom: 15px;
}
</style>
