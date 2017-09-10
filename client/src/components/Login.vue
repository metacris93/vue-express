<template>   
  <v-layout row>
    <v-flex xs6 offset-xs3>
      <div class="white elevation-2">
        <v-toolbar flat dense class="cyan" dark>
          <v-toolbar-title>Register</v-toolbar-title>
        </v-toolbar> 
  
        <div class="pl-4 pr-4 pt-2 pb-2">
          <v-form action="" method="post">
            <v-text-field
              label="Email"
              name="email"
              type="email"
              v-model="email"                  
              required
            ></v-text-field>               
            <v-text-field
              label="Password"
              name="Password"
              v-model="password"                  
              :append-icon="see_password ? 'visibility' : 'visibility_off'"
              :append-icon-cb="() => (see_password = !see_password)"
              :type="see_password ? 'password' : 'text'"                
              required
            ></v-text-field>
            <v-btn class="cyan white--text" @click="login">Login</v-btn><br>
          </v-form>  
          <div class="error" v-html="error"></div>   
        </div> 
      </div>
    </v-flex>  
  </v-layout>   
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'
export default {
  data () {
    return {
      email: '',
      password: '',
      error: null,
      see_password: false
    }
  },
  watch: {
    email (value) {
      console.log('email has changed', value)
    }
  },
  methods: {
    async login () {
      try {
        await AuthenticationService.login({
          email: this.email,
          password: this.password
        })
      } catch (error) {
        this.error = error.response.data.error
      }
    }
  }
}
</script>

<style scoped>
  .error {
    color: red;
  }
</style>
