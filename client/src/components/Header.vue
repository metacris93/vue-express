<template>
  <v-toolbar fixed class="cyan" dark> 
    <v-toolbar-title class="white--text mr-4">
      <span @click="navigateTo({name: 'root'})" class="home">TabTracker</span>
    </v-toolbar-title>

    <v-toolbar-items>
      <v-btn 
        @click="navigateTo({name: 'songs'})"
        flat dark>
        Browse
      </v-btn>
    </v-toolbar-items>

    <v-spacer></v-spacer>

    <v-toolbar-items>
      <v-btn 
        v-if="!$store.state.isUserLoggedIn"
        flat dark to="login">
        Login
      </v-btn>
    </v-toolbar-items>

    <v-toolbar-items>
      <v-btn 
        v-if="!$store.state.isUserLoggedIn"
        flat dark to="register">
        Sign up
      </v-btn>
    </v-toolbar-items>

    <v-toolbar-items>
      <v-btn 
        v-if="$store.state.isUserLoggedIn"
        flat dark @click="logout">
        Log out
      </v-btn>
    </v-toolbar-items>
  </v-toolbar>
</template>

<script>
export default {
  methods: {
    navigateTo (route) {
      this.$router.push(route)
    },
    logout () {
      this.$store.dispatch('setToken', null)
      this.$store.dispatch('setUser', null)
      this.$router.push({name: 'root'})
    }
  }
}
</script>

<style scoped>
  .home {
    cursor: pointer;
  }
</style>
