<template>
  <div class="user-profile">
    <div class="user-profile__sidebar">
      <div class="user-profile__user-panel">
        <h1 class="user-profile__username">@{{ user.username }}</h1>
        <div class="user-profile__admin-badge" v-if="user.isAdmin">Admin</div>
        <div class="user-profile__non-admin-badge" v-else>Not Admin</div>
        <div class="user-profile__follower-count">
          <strong>Followers: </strong> {{ followers }}
        </div>
        <form class="user-profile__newtwoot"  @submit.prevent="createNewTwoot">
          <label for="newtwoot"><strong>New Twoot</strong></label>
          <textarea id="newtwoot" rows="4" v-model="newTwootContent"/>
          <label for="newTwootType">Type</label>
          <select id="newTwootType" v-model="newTwootType">
            <option :value="option.value" 
                    v-for="option in twootTypes" 
                    :key="option.value">
                    {{ option.name }}
            </option>
          </select>
          <button>
            Twoot!!
          </button>
        </form>
      </div>
    </div>
    <div class="user-profile__twoots-wrapper">
      <TwootItem v-for="twoot in user.twoots" 
        :key="twoot.id" 
        :twoot="twoot" 
        :username="user.username" 
        @favorite="toggleFavorite"/>
    </div>
  </div>
</template>

<script>

import TwootItem from './TwootItem.vue'

export default {
  name: 'UserProfile',
  components:{
    TwootItem 
  },
  data() {
    return{
      newTwootContent:'',
      newTwootType:'instant',
      twootTypes:[
        {value:"draft", name:"Draft"},
        {value:"instant", name:"Instant Twoot"}

      ],
      is_loading: false,
      followers: 0,
      user:{
        id: 0,
        username: '_juanillo',
        firstname: 'juanillo',
        lastname: 'total',
        email: 'jt@gmail.com',
        isAdmin: false ,
        twoots: [
          {id:1, content: "twoots is amazing."},
          {id:2, content: "subscribe to 'The end of world!'"}
        ]
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
    },
    toggleFavorite(id){
      console.log(`New favorite #${id}`);
    },
    createNewTwoot(){
      if(this.newTwootContent && this.newTwootType!=='draft'){
        this.user.twoots.unshift({
          id: this.user.twoots.length,
          content: this.newTwootContent
        })
        this.newTwootContent = '';
      }
    }
  },
  mounted(){
    this.followers = 1;
  }
}
</script>

<style>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;
}
.user-profile__user-panel {
  display: flex;
  flex-direction: column;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #DFE3E8;
  margin-bottom: auto;
}

.user-profile__newtwoot {
  margin: 20px;
  display: flex;
  flex-direction: column;
}

h1 {
  margin: 0;
}
.user-profile__admin-badge, .user-profile__non-admin-badge {
  background: rebeccapurple;
  color: white;
  border-radius: 5px;
  margin-right: auto;
  padding: 0 10px;
  font-weight: bold;
}
.user-profile__admin-badge {
  background: rgb(106, 131, 58);
}
.user-profile__twoots-wrapper {
  display: grid;
  grid-gap: 10px;
  margin-bottom: auto;
  color: white;
}
 
</style>
