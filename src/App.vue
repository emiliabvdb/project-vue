<template>
  <div id="app">
    <div id="nav">
      <h1>{{appName}}</h1>
      <router-link to="/">Home</router-link> |
      <router-link v-if="authenticated" to="/myprofile">My profile</router-link>
      <router-link v-else to="/Login" class="s">My profile</router-link> |
      <router-link to="/about">Om oss</router-link> |
      <router-link v-if="authenticated" to="/Login" v-on:click.native="logout()" replace> Logout </router-link>
      <router-link v-else to="/Login" v-on:click.native="logout()" replace> Login </router-link>

    </div>
    <router-view @authenticated="setAuthenticated" />
  </div>
</template>


<script>
  export default {
    name: 'profile',
    data () {
      return {
        appName: 'The Auction Application',
        authenticated: false,
        mockAccount: {
            username: "emilia",
            password: "emilie"
        }
      }
    },
//    mounted() {}, første som skjer på siden

    methods: {
      setAuthenticated(status) {
          this.authenticated = status;
      },
      logout() {
          this.authenticated = false;
      }
    }
  };
</script>


<style>

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
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
  text-decoration: none;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
#nav a.router-link-exact-active.s {
  color: #2c3e50;
}
</style>
