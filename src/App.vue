<template>
  <div id="app">
    <user-profile></user-profile>
  </div>
</template>

<script>
import UserProfile from './components/UserProfile.vue'

export default {
  components: {
    UserProfile
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #2c3e50;
  margin-top: 60px;
}
</style>
