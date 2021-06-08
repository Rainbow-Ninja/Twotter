<template>
  <div id='app'>
    @{{ user.username }} - {{ fullName }}
    <strong>Followers: </strong>{{ followers }}
    <!-- <button v-on:click="followUser">Follow</button> these two lines are the same!! --> 
    <button @click="followUser">Follow</button>
  </div>
</template>

<script>


export default {
  name: 'App',
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
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    }
  },
  methods: {
    followUser() {
      this.followers++;
    }
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
  display: flex;
  flex-direction: column;
}
</style>
