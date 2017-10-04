<template>
  <v-layout column>
    <v-flex xs4 offset-xs4>
      <panel title="Login">
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
                type="submit" @click="login"> Login
        </v-btn>
      </panel>
    </v-flex>
  </v-layout>
</template>

<script>
  import AuthenticationService from '@/services/AuthenticationService'
  import Panel from '@/components/Panel'
  export default {
    name: 'login',
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
      async login () {
        try {
          const response = await AuthenticationService.login({
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
