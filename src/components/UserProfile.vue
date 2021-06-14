<template>
  <div class='user-profile'>
    <div class='user-profile__user-panel'>
      <h1 class='user-profile__username'>@{{ user.username }}</h1> 
      <div class='user-profile__admin-badge' v-if="user.isAdmin">Admin</div> <!-- will only show ifAdmin is true -->
      <div class='user-profile__admin-badge' v-else>Not Admin</div> <!-- will only show ifAdmin is false -->
        <div class='user-profile__follower-count'>
          <strong>Followers: </strong>{{ followers }}
        <!-- <button v-on:click="followUser">Follow</button> 
        <button @click="followUser">Follow</button>  these two lines are the same!! --> 
        </div>
        <form class="user-profile__create-twoot" @submit.prevent="createNewTwoot" :class="{ '--exceeded': newTwootCharCount > 180 }"> <!-- add the class exceeded when that condition is met -->
            <label for="newTwoot"><strong>New Twoot</strong> ({{ newTwootCharCount }}/180) </label>
            <textarea id="newTwoot" rows="4" v-model="newTwootContent" />
            <div class="user-profile__create-twoot-type">
                <label for="newTwootType"><strong>Type: </strong></label>
                <select id="newTwootType" v-model="selectedTwootType">
                    <option :value="option.value" v-for="(option, index) in twootTypes" :key="index">
                        {{ option.name }}
                    </option>
                </select>
            </div>
            <button>
                Twoot!
            </button>
        </form>
      </div>
      <div class="user-profile__twoots-wrapper">
        <TwootItem 
            v-for="twoot in user.twoots" 
            :key="twoot.id" 
            :username="user.username" 
            :twoot="twoot" 
            @fav="toggleFav" 
        />
      </div>
    </div>
</template>

<script>
import TwootItem from "./TwootItem";

export default {
  name: 'UserProfile',
  components: { TwootItem },
  data() {
    return {
      newTwootContent: '',
      selectedTwootType: 'instant',
      twootTypes: [
        {value: 'draft', name: 'Draft'},
        {value: 'instant', name: 'Instant Twoot'}
      ],
      followers: 0,
      user: {
        id: 1,
        username: 'CodeTravelled',
        firstName: 'Jo',
        lastName: 'Dunham',
        email: 'joDunham@email.com',
        isAdmin: false,
        twoots: [
            { id: 1, content: "Twotter is Amazing!" },
            { id: 2, content: "Don't forget to follow @CodeTravelled!" },
            { id: 3, content: "Jo is awesome!" },
            { id: 4, content: "My kitties are adorbs <3" }
        ]
      }
    }
  },
  watch: { //watches something and runs every time it changes
    followers(newFollowerCount, oldFollowerCount) { //give it the same name as what you are watching just to make it readable
      if(oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} has gained a follower!`);
      }
    }
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
    newTwootCharCount() {
        return this.newTwootContent.length;
    }
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFav(id) {
        console.log(`Favourited Twoot #${id}`);
    },
    createNewTwoot() {
        if(this.newTwootContent && this.selectedTwootType !== 'draft') {
            this.user.twoots.unshift({
                id: this.user.twoots.length + 1,
                content: this.newTwootContent
            })
            this.newTwootContent='';
        }
    }
  },
  
  mounted() { //run every time component is loaded for the first time, or remounted, each time starts the first time. Lifecycle hook
    this.followUser();
  }
}
</script>

<style lang="scss" scoped>
    .user-profile {
        display: grid;
        grid-template-columns: 1fr 3fr;
        width: 100%;
        padding: 50px 5%;

        .user-profile__user-panel{
            display: flex;
            flex-direction: column;
            margin-right: 50px;
            padding: 20px;
            background-color: white;
            border-radius: 5px;
            border: 1px solid #DFE3E8;

            h1 {
                margin: 0;
            }

            .user-profile__admin-badge {
                background-color: rebeccapurple;
                color: white;
                border-radius: 5px;
                margin-right: auto;
                padding: 0 10px;
                font-weight: bold;
                margin-bottom: 20px;
            }

            .user-profile__create-twoot {
                padding-top: 20px;
                display: flex;
                flex-direction: column;

                &.--exceeded {
                    color: red;
                    border-color: red;

                    button {
                        background-color: red;
                        border: none;
                        color: white;
                    }
                }
            }
                
            .user-profile__twoots-wrapper {
                display: grid;
                grid-gap: 10px;
            }
        }
    }

</style>