<template>  
    <div>
    
          <v-avatar v-if="loged" @click="goToInspire" size="36px" slot="activator">
            <img src="https://avatars0.githubusercontent.com/u/9064066?v=4&s=460"  alt="">
          </v-avatar>
          <strong>{{ username }}</strong>                              
          <v-btn v-if="loged" @click="home">
            <v-icon>home</v-icon>
          </v-btn>
          <dialog-login  v-if="!loged"></dialog-login>
          <v-btn  v-if="!loged">Facebook</v-btn>
          
    </div>
</template>

<script>
import axios from 'axios'
import dialogLogin from '~/components/DialogLogin.vue'

export default {
  data () {
    return {
      username: '',
      loged: false
    }
  },
  mounted () {
    this.getUsername()
  },
  components: {
    dialogLogin
  },
  methods: {
    getUsername () {
      axios({
        method: 'get',
        url: 'http://localhost:8080/getUsername',
        headers: {'Content-Type': 'application/json'},
        params: {
          access_token: this.getCookie('access_token')
        }
      }).then(function (response) {
        if (response) {
          if (this.getCookie('access_token')) {
            this.username = response.data
            this.loged = true
            this.$emit('hasUser')
          }
        }
      }.bind(this))
    },
    getCookie (name) {
      var value = '; ' + document.cookie
      var parts = value.split('; ' + name + '=')
      if (parts.length === 2) return parts.pop().split(';').shift()
    },
    goToInspire () {
      this.$router.push('/inspire')
    },
    home () {
      this.$router.push('/')
    }
  }
}
</script>
