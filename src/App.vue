<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link>
      |
      <router-link to="/posts">Posts</router-link>
      |
      <router-link v-if="loggedIn()" to="/posts/new">New Post</router-link>
      |
      <router-link v-if="!loggedIn()" to="/signup">Signup</router-link>
      |
      <router-link v-if="!loggedIn()" to="/login">Login</router-link>
      |
      <router-link v-if="loggedIn()" to="/logout">Logout</router-link>
    </div>
    <div v-if="flashMessage">
      {{ flashMessage }}
      <button v-on:click="flashMessage = ''">X</button>
    </div>
    <router-view />
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>

<script>
export default {
  data: function() {
    return {
      flashMessage: "",
    };
  },
  methods: {
    loggedIn: function() {
      return localStorage.jwt;
    },
    getUserId: function() {
      return localStorage.user_id;
    },
  },
};
</script>
