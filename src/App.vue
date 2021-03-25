<template>
  <div id="app">
    @{{ user.username }}:  {{ fullname }}
    <br />
    Followers: {{ followers }}
    <br />
    <button @click="onclick();">Click Me!</button>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return{
      is_loading: false,
      followers: 0,
      user:{
        id: 0,
        username: '_ juanillo',
        firstname: 'juanillo',
        lastname: 'total',
        email: 'jt@gmail.com',
        isAdmin: true
      }
    }
  },
  watch:{
    followers(newvalue, oldvalue){
      if(oldvalue < newvalue){
        console.log(`${this.user.username} has gained a follower.`);
      }
    }
  },
  computed:{
    fullname(){
      return `${this.user.firstname} ${this.user.lastname}`
    } 
  },
  methods:{
    onclick: function(){
      this.followers++;
    }
  },
  mounted(){
    this.followers = 1;
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
  margin-top: 60px;
}
</style>
