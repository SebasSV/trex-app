<template>  
    <v-dialog v-model="dialog" persistent max-width="500px">
      <v-btn slot="activator">Login</v-btn>
      <v-card>
        <v-card-title>
          <span class="headline">Login</span>
        </v-card-title>
        <v-card-text>
          <v-container grid-list-md>
            <v-layout wrap>              
              <v-flex xs12>
                <v-text-field v-model="username" label="User Name" required></v-text-field>
              </v-flex>
              <v-flex xs12>
                <v-text-field v-model="password" label="Password" type="password" required></v-text-field>
              </v-flex>                        
            </v-layout>
          </v-container>
          <small>Forgot pasword?</small>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" flat @click="dialog = false">Close</v-btn>
          <v-btn color="blue darken-1" flat @click="login">Login</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      username: '',
      password: '',
      dialog: false
    }
  },
  methods: {
    login () {
      var params = new URLSearchParams()
      params.append('grant_type', 'password')
      params.append('username', this.username)
      params.append('password', this.password)
      axios({
        method: 'post',
        url: 'http://localhost:8080/oauth/token',
        auth: {username: 'my-trusted-client', password: 'secret'},
        headers: {'Access-Control-Allow-Origin': '*', 'Access-Control-Allow-Methods': 'GET, POST, PATCH, PUT, DELETE, OPTIONS', 'Access-Control-Allow-Headers': 'Origin, Content-Type, X-Auth-Token', 'Content-type': 'application/x-www-form-urlencoded'},
        data: params
      }).then(function (response) {
        if (response) {
          this.dialog = false
          document.cookie = 'access_token=' + response.data.access_token + ';path=/'
          document.location.replace('/')
        }
      }.bind(this))
    }
  }
}
</script>
