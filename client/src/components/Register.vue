<template>
  <v-content>
    <v-container fluid fill-height>
      <v-layout align-center justify-center>
        <v-flex xs12 sm8 md6>
          <panel title="Register">
            <v-card-text>
              <v-form>
                <v-text-field v-model="email" name="email" label="E-Mail" type="text"></v-text-field>
                <v-text-field v-model="password" id="password" name="password" label="Password" type="password"></v-text-field>
              </v-form>
            </v-card-text>
            <div class="error" v-html="error" />
            <br>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn @click="register" dark color="teal">Register</v-btn>
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
    async register () {
      try {
        const response = await AuthenticationService.register({
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
