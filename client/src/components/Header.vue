<template>
  <v-toolbar fixed class="purple" dark>
    <v-toolbar-title class="mr-4">
      <v-btn flat @click="navigateTo({name: 'root'})">TabTracker</v-btn>
    </v-toolbar-title>
    <v-toolbar-items>
      <v-btn flat dark @click="navigateTo({name: 'songs'})" > Browse </v-btn>
    </v-toolbar-items>
    <v-spacer></v-spacer>
    <v-toolbar-items >
      <template v-if="!$store.state.isUserLoggedIn">
      <v-btn flat dark @click="navigateTo({name: 'login'})" > Login </v-btn>
      <v-btn flat dark @click="navigateTo({name: 'register'})"> SignUp </v-btn>
      </template>
      <template v-else>
        <v-btn flat dark @click="logout"> Logout </v-btn>
      </template>
    </v-toolbar-items>

  </v-toolbar>
</template>
<script>
  export default{
    name: 'header',
    data () {
      return {
        msg: 'hello vue'
      }
    },
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
