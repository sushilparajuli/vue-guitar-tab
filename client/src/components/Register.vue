<template>
  <v-layout column>
    <v-flex xs4 offset-xs4>
      <panel title="Register">
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
      </panel>

    </v-flex>
  </v-layout>

</template>

<script>
  import AuthenticationService from '@/services/AuthenticationService'
  import Panel from '@/components/Panel'
  export default {
    name: 'register',
    components: {
      Panel
    },
    data () {
      return {
        email: '',
        password: '',
        error: null
      }
    },
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
