<template>
  <div class='user-profile'>
    <div class='user-profile__user-panel'>
      <h1 class='user-profile__username'>@{{ user.username }}</h1> 
        <div class='user-profile__follower-count'>
          <strong>Followers: </strong>{{ followers }}
    <!-- <button v-on:click="followUser">Follow</button> 
    <button @click="followUser">Follow</button>  these two lines are the same!! --> 
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
        isAdmin: true
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

    h1 {
        margin: 0;
    }
</style>