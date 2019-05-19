<template>
  <v-content>
    <v-container fluid fill-height>
      <v-layout align-center justify-center>
        <v-flex xs12 sm8 md6>
          <panel title="Login">
            <v-card-text>
              <v-form>
                <v-text-field v-model="email" name="email" label="E-Mail" type="email"></v-text-field>
                <v-text-field v-model="password" id="password" name="password" label="Password" type="password"></v-text-field>
              </v-form>

            </v-card-text>
            <div class="error" v-html="error" />
            <br>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn @click="login" dark color="teal">Login</v-btn>
            </v-card-actions>
          </panel>
        </v-flex>
      </v-layout>
    </v-container>
  </v-content>
</template>

<script>
import AuthenticationService from '../services/AuthenticationService'
import Panel from '@/components/Panel'

export default {
  data () {
    return {
      email: '',
      password: '',
      error: null
    }
  },
  components: {
    Panel
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
      } catch (error) {
        this.error = error.response.data.error
      }
    }
  }
}
</script>

<style scoped>
</style>
