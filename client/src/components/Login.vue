<template>   
  <v-layout row>
    <v-flex xs6 offset-xs3>
      <panel title="Log in">
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
      </panel>      
    </v-flex>  
  </v-layout>   
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'
import Panel from '@/components/Panel'
export default {
  data () {
    return {
      email: '',
      password: '',
      error: null,
      see_password: true
    }
  },
  components: {
    Panel
  },
  /* watch: {
    email (value) {
      console.log('email has changed', value)
    }
  }, */
  methods: {
    async login () {
      try {
        const response = await AuthenticationService.login({
          email: this.email,
          password: this.password
        })
        this.$store.dispatch('setToken', response.data.token)
        this.$store.dispatch('setUser', response.data.user)
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
