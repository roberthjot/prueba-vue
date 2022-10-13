<template>
  <imagesUpload msg="Welcome to Your Vue.js App"/>
</template>

<script>
import imagesUpload from './components/imagesUpload.vue'

export default {
  name: 'App',
  components: {
    imagesUpload
  }
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
