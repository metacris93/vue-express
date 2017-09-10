<template>
  <v-toolbar fixed class="cyan" dark> 
    <v-toolbar-title class="white--text mr-4">
      <span @click="navigateTo({name: 'root'})" class="home">TabTracker</span>
    </v-toolbar-title>

    <!--<v-toolbar-items>
      <v-btn flat dark>
        Browse
      </v-btn>
    </v-toolbar-items> -->

    <v-spacer></v-spacer>
    <v-toolbar-items>
      <v-btn flat dark to="login">
        Login
      </v-btn>
    </v-toolbar-items>

    <v-toolbar-items>
      <v-btn flat dark to="register">
        Sign up
      </v-btn>
    </v-toolbar-items>
  </v-toolbar>
</template>

<script>
export default {
  methods: {
    navigateTo (route) {
      this.$router.push(route)
    }
  }
}
</script>

<style scoped>
  .home {
    cursor: pointer;
  }
</style>
