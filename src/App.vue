<template>
<nav>
      <router-link to="/">
        <div class="navigation__logo">
          Twotter
        </div>
      </router-link>
      <router-link v-for="user in users" :key="user.id" :to="{ name:'UserProfile', params: { userId: user.id } }" >
        <div class="navigation__user">
          {{ user.username }}
        </div>
      </router-link>
    </nav>

  <div id="app">
-    <router-view/>
  </div>
  
</template>

<script>

  import { users } from '@/assets/users.js'
  export default {
    setup(){
      return {
        users
      }
    }
  }
</script>

<style lang="scss">
#app {
  background-color: #2c3e50;
  margin-top: 60px;
}

nav {
  background-color: aqua;
}
</style>