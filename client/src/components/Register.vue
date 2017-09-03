<template>
  <div>
    <h1>Register</h1>
    <!--<form action="" method="post">-->
      <input type="email" v-model="email" name="email" placeholder="email" required><br>
      <input type="password" v-model="password" name="password" placeholder="password" required><br>
      <input type="submit" @click="register" name="submit">
    <!--</form>-->    
  </div>
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'
export default {
  data () {
    return {
      email: 'abc@abc.com',
      password: '123456'
    }
  },
  watch: {
    email (value) {
      console.log('email has changed', value)
    }
  },
  methods: {
    async register () {
      await AuthenticationService.register({
        email: this.email,
        password: this.password
      })
    }
  }
}
</script>

<style scoped>

</style>
