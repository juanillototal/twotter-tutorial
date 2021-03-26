<template>
  <div class="user-profile">
    <div class="user-profile__sidebar">
      <div class="user-profile__user-panel">
        <h1 class="user-profile__username">@{{ state.user.username }}</h1>
        <div class="user-profile__admin-badge" v-if="state.user.isAdmin">Admin</div>
        <div class="user-profile__non-admin-badge" v-else>Not Admin</div>
        <div class="user-profile__follower-count">
          <strong>Followers: </strong> {{ state.followers }}
        </div>
        <form class="user-profile__newtwoot"  @submit.prevent="createNewTwoot" :class="{ '--exceeded': newtwootcharcount > 180 }">
          <label for="newtwoot"><strong>New Twoot</strong> {{ newtwootcharcount }}/180</label>
          <textarea id="newtwoot" rows="4" v-model="state.newTwootContent"/>
          <label for="newTwootType">Type</label>
          <select id="newTwootType" v-model="state.newTwootType">
            <option :value="option.value" 
                    v-for="option in state.twootTypes" 
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
      <TwootItem v-for="twoot in state.user.twoots" 
        :key="twoot.id" 
        :twoot="twoot" 
        :username="state.user.username" 
        @favorite="toggleFavorite"/>
    </div>
  </div>
</template>

<script>

import TwootItem from './TwootItem.vue'
import { reactive, computed } from 'vue'

export default {
  name: 'UserProfile',
  components:{
    TwootItem 
  },
  setup(){
    const state = reactive({
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
        isAdmin: true ,
        twoots: [
          {id:1, content: "twoots is amazing."},
          {id:2, content: "subscribe to 'The end of world!'"}
        ]
      }
    }
    );

    const newtwootcharcount = computed(() => state.newTwootContent.length );
    const fullname = computed(() => `${state.user.firstname} ${state.user.lastname}` );

    function onclick(){
      this.followers++;
    }

    function toggleFavorite(id){
      console.log(`New favorite #${id}`);
    }

    function createNewTwoot(){
      if(state.newTwootContent && state.newTwootType!=='draft'){
        state.user.twoots.unshift({
          id: state.user.twoots.length,
          content: state.newTwootContent
        })
        state.newTwootContent = '';
      }
    }

    return {
      state, 
      newtwootcharcount,
      fullname,
      toggleFavorite,
      createNewTwoot,
      onclick
      };
    }
  }
</script>

<style lang="scss" scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;

  .user-profile__user-panel {
    display: flex;
    flex-direction: column;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3E8;
    margin-bottom: auto;
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

    .user-profile__newtwoot {
      margin: 20px;
      display: flex;
      flex-direction: column;
      &.--exceeded {
        color: red;
        border-color: red;
        button {
          color: white;
          background: red;
          border: none;
        }
      }
    }
  }
  .user-profile__twoots-wrapper {
    display: grid;
    grid-gap: 10px;
    margin-bottom: auto;
    color: white;
  }
}
</style>
