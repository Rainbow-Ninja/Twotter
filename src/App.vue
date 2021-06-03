<template>
  <div id='app'>
    @{{ user.username }}
  </div>
</template>

<script>


export default {
  name: 'App',
  date() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: 'CodeTravelled',
        firstName: 'Jo',
        lastname: 'Dunham',
        email: 'joDunham@email.com',
        isAdmin: true
      }
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
  margin-top: 60px;
}
</style>
