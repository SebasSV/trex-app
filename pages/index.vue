<template>

  <div id="e3" style="max-width: 550px; margin: auto;" class="grey lighten-3" >

    <v-container fluid style="min-height: 0;" grid-list-lg>
      <v-layout row wrap>
        
        <v-flex xs12>        
          <v-card color="blue-grey darken-2" class="white--text">
            <v-card-title primary-title>
              <div class="headline">Unlimited music now</div>
              <div>Listen to your favorite artists and albums whenever and wherever, online and offline.</div>
            </v-card-title>
            <v-card-actions>
              <v-btn flat dark>Listen now</v-btn>
            </v-card-actions>
          </v-card>
        </v-flex>

        <!-- <v-flex xs12 id="root" v-for="post in posts" :key"post.id" >
          <v-card color="blue-grey darken-2" class="white--text">
            <v-container fluid grid-list-lg>
              <v-layout>
                <v-flex>
                  <div>
                    <div class="headline">Supermodel</div>
                    <div>{{post.name}}</div>
                  </div>
                </v-flex>
              </v-layout>

              <v-layout row>          
                <v-flex>
                  <div>{{post.body}}</div>
                  <v-card-media
                    src="/bby-driver.jpg"
                    height="300px"
                    contain
                  ></v-card-media>
                </v-flex>
              </v-layout>  

            </v-container>
          </v-card>
        </v-flex> -->
        

      </v-layout>
    </v-container>
  </div>
</template>

<script>
import axios from 'axios'
import Vue from 'vue'

var app = new Vue({
  el: '#root',
  data: {posts: []},
  mounted () {
    this.fetchPosts()
  },
  methods: {
    fetchPosts () {
      axios.get('/posts').then(function (response) {
        this.posts = response.data
      }).bind(this)
    }
  }
})

export default {
  async asyncData ({ params }) {
    let { data } = await axios.get(`localhost8080:/post`)
    return { title: data.name }
  },
  data () {
    return {
      clipped: false,
      drawer: true,
      fixed: false,
      items: [
        { icon: 'apps', title: 'Welcome', to: '/' },
        { icon: 'bubble_chart', title: 'Inspire', to: '/inspire' }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Tres-App'
    }
  }
}
</script>
