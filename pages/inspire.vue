<template>
  <div>
    <v-container grid-list-md text-xs-center fluid>
      <v-layout row wrap>
        <v-flex xs12>
            <v-card color="blue-grey darken-2" class="white--text">
                <v-container fluid grid-list-lg>              
                  <v-layout row>          
                    <v-flex>                        
                      <v-card-media src="/bby-driver.jpg" height="300px" contain></v-card-media>
                    </v-flex>
                  </v-layout>  
                </v-container>
            </v-card>
        </v-flex>
      </v-layout>
    </v-container>

      <div id="e3" style="max-width: 550px; margin: auto;" class="grey lighten-3" >
        <v-container fluid style="min-height: 0;" grid-list-lg>
          <v-layout row wrap> 
            <index-cards-user></index-cards-user>   
          </v-layout>
        </v-container> 
      </div>
    </div>        
</template>

<script>
import indexCardsUser from '~/components/IndexCardsUser.vue'
import axios from 'axios'

export default {
  data () {
    return {
      childState: false
    }
  },
  components: {
    indexCardsUser
  },
  mounted () {
    this.loadUserOptions()
  },
  methods: {
    publishPost () {
      axios({
        method: 'post',
        url: 'http://localhost:8080/post',
        headers: {'Content-Type': 'application/json'},
        data: {
          name: 'name',
          body: this.body
        },
        params: {
          access_token: this.getCookie('access_token')
        }
      }).then(function (response) {
        if (response) {
          console.log(response)
          this.childState = true
          this.dialog = false
          this.body = ''
        }
      }.bind(this))
    },
    getCookie (name) {
      var value = '; ' + document.cookie
      var parts = value.split('; ' + name + '=')
      if (parts.length === 2) return parts.pop().split(';').shift()
    },
    lockChild () {
      this.childState = false
    },
    loadUserOptions () {
      if (this.getCookie('access_token')) {
        this.loged = true
      }
    }
  }
}
</script>

