<template>
  <div id="app">
    <router-view class="min-height"/>
    <my-footer/>
  </div>
</template>

<script>
import MyFooter from './components/Footer'
export default {
  name: 'App',
  components: {MyFooter}
}
</script>

<style>
  #app {
    font-family: 'Lucida Sans Unicode', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    text-align: center;
  }
  .min-height {
    min-height: 90vh;
  }
</style>
