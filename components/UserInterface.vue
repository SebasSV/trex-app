<template>  
    <div>{{ username }}</div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      username: ''
    }
  },
  mounted () {
    this.getUsername()
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
            this.$emit('hasUser')
          }
        }
      }.bind(this))
    },
    getCookie (name) {
      var value = '; ' + document.cookie
      var parts = value.split('; ' + name + '=')
      if (parts.length === 2) return parts.pop().split(';').shift()
    }
  }
}
</script>
