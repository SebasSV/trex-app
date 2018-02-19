<template>

<div class="flex xs12">
    <v-flex xs12 v-for="post in posts" :key="post.id">
        <v-card color="blue-grey darken-2" class="white--text">    
            <v-container fluid grid-list-lg>              
              <v-layout row wrap> 
                <v-flex xs2>
                  <v-avatar  size="36px" slot="activator">
                    <img :src="post.avatarUrl"  alt="">
                  </v-avatar>                        
                </v-flex>
                <v-flex xs3 d-flex>
                  <v-layout row wrap class="text-lg-left">                  
                    <v-flex d-flex class="pb-0 pt-0">                      
                        <strong>{{post.username}} {{post.lastName}}</strong>                                         
                    </v-flex>
                    <v-flex d-flex class="pb-0 pt-0">                       
                        <strong>{{post.profession}}</strong>                              
                    </v-flex>
                    <v-flex d-flex class="pb-0 pt-0">                       
                        <strong>{{post.createdDate}}</strong>                       
                    </v-flex>
                  </v-layout>                       
                </v-flex>
              </v-layout>                       
              <v-layout row>          
                    <v-flex>            
                      <v-card-title primary class="title">{{post.body}}</v-card-title>                                  
                      <v-card-media src="/bby-driver.jpg" height="300px" contain></v-card-media>
                    </v-flex>
              </v-layout>  
            </v-container>
        </v-card>
    </v-flex>
</div>

</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      posts: [],
      counter: 0
    }
  },
  mounted () {
    this.fetchUserData()
  },
  methods: {
    fetchUserData () {
      axios({
        method: 'get',
        url: 'http://localhost:8080/userPost/id',
        headers: {'Content-Type': 'application/json'},
        params: {
          access_token: this.getCookie('access_token')
        }
      }).then(function (response) {
        this.posts = response.data
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
