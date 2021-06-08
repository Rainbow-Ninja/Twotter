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
      </div>
      <div class="user-profile__twoots-wrapper">
        <div class="user-profile__twoot" v-for="twoot in user.twoots" :key="twoot.id">
            {{ twoot.content }}
        </div>
      </div>
    </div>
</template>

<script>
export default {
  name: 'UserProfile',
  data() {
    return {
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
    }
  },
  methods: {
    followUser() {
      this.followers++;
    }
  },
  
  mounted() { //run every time component is loaded for the first time, or remounted, each time starts the first time. Lifecycle hook
    this.followUser();
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

    .user-profile__user-panel{
        display: flex;
        flex-direction: column;
        margin-right: 50px;
        padding: 20px;
        background-color: white;
        border-radius: 5px;
        border: 1px solid #DFE3E8;
    }

    .user-profile__admin-badge {
        background-color: rebeccapurple;
        color: white;
        border-radius: 5px;
        margin-right: auto;
        padding: 0 10px;
        font-weight: bold;
    }

    h1 {
        margin: 0;
    }
</style>