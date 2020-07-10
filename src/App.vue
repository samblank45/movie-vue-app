<template>
  <div id="app">

    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <router-link class="navbar-brand" to="/">Home</router-link>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent"       aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>

    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav mr-auto">
        <li class="nav-item active">
          <router-link class="nav-link" to="/movies">Movies </router-link>
        </li>
        <!-- logged in and cannot see login -->
        <li v-if="!isLoggedIn()" class="nav-item active">
          <router-link class="nav-link" to="/login">Login </router-link>
        </li>
        <!-- logged in and cannot see signup -->
        <li v-if="!isLoggedIn()" class="nav-item active">
          <router-link class="nav-link" to="/signup">Signup </router-link>
        </li>
        <li class="nav-item active">
          <router-link class="nav-link" to="/movies/new">New Movie </router-link>
        </li>
        <!-- Not logged in and cannost see logout -->
        <li v-if="isLoggedIn()" class="nav-item active">
          <router-link class="nav-link" to="/logout">Logout </router-link>
        </li>
      </ul>
    </div>
  </nav>
    <router-view/>
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
  methods: {
    isLoggedIn: function() {
      return localStorage.getItem("jwt");
    }
  }
};
</script>
