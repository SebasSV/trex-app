<template>

<div class="flex xs12">
    <v-flex xs12 v-for="post in posts" :key="post.id">
        <v-card color="blue-grey darken-2" class="white--text">
            <v-container fluid grid-list-lg>
                <!-- <v-layout>
                    <v-flex>
                        <div>
                            <div class="headline">Supermodel</div>
                            <div>{{post.name}}</div>
                        </div>
                    </v-flex>
                </v-layout> -->

              <v-layout row>          
                    <v-flex>
                        <div>{{post.body}}</div>
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
      posts: []
    }
  },
  mounted () {
    this.fetchPosts()
  },
  methods: {
    fetchPosts () {
      console.log('entro')
      return axios.get('http://localhost:8080/posts')
        .then(function (response) {
          this.posts = response.data
        }.bind(this))
    }
  },
  watch: {
    '$route': 'fetchPosts'
  }
}
</script>
