<template>
  <v-toolbar fixed dark class="teal">
    <v-toolbar-title class="mr-4">
      <span @click="navigateTo({name: 'root'})">
        TabTracker
      </span>
    </v-toolbar-title>

    <!-- TODO: Implement Me -->
    <!-- <v-toolbar-items>
      <v-btn flat dark>
        Browse
      </v-btn>
    </v-toolbar-items> -->
    <v-spacer></v-spacer>
    <v-toolbar-items>
      <v-btn v-if="!$store.state.isUserLoggedIn" @click="navigateTo({name: 'login'})" flat dark>
        Login
      </v-btn>
      <v-btn v-if="!$store.state.isUserLoggedIn" @click="navigateTo({name: 'register'})" flat dark>
        Sign Up
      </v-btn>
    </v-toolbar-items>
  </v-toolbar>
</template>

<script>

export default {
  data () {
    return {}
  },
  methods: {
    navigateTo (route) {
      this.$router.push(route)
    }
  }
}
</script>

<style scoped>

</style>
