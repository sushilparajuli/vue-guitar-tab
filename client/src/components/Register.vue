<template>
  <v-layout column>
    <v-flex xs4 offset-xs4>
      <v-card dark class="grey lighten-2">
        <v-toolbar flat dense class="primary" dark>
          <v-toolbaar-title class="white--text"><h6 class="mb-0"> Register </h6> </v-toolbaar-title>
        </v-toolbar>
        <div class="pl-5 pr-5 pb-4">
          <v-text-field
                  type="email"
                  name="email"
                  label="Email"
                  id="email"
                  v-model="email"
                  required
          ></v-text-field>
          <v-text-field
                  type="password"
                  name="password"
                  label="Password"
                  id="password"
                  v-model="password"
                  required
          ></v-text-field>


          <v-alert v-if="error" v-html="error" error value="true">
          </v-alert>

          <v-btn
                  success
                  dark
                  type="submit" @click="register"> Register</v-btn>
        </div>
      </v-card>
    </v-flex>
  </v-layout>

</template>

<script>
  import AuthenticationService from '@/services/AuthenticationService'
  export default {
    name: 'hello',
    data () {
      return {
        email: '',
        password: '',
        error: null
      }
    },

    /* watch: {
     email (value) {
     console.log('email has changed', value)
     }

     }, */
    methods: {
      async register () {
        try {
          const response = await AuthenticationService.register({
            email: this.email,
            password: this.password
          })
          this.$store.dispatch('setToken', response.data.token)
          this.$store.dispatch('setUser', response.data.user)
        } catch (err) {
          this.error = err.response.data.error
        }
      }

    }
  }

</script>
<style scoped>

</style>
