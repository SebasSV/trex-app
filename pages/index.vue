<template>

  <div id="e3" style="max-width: 550px; margin: auto;" class="grey lighten-3" >
    <v-container fluid style="min-height: 0;" grid-list-lg>
      <v-layout row wrap> 

        <v-flex xs12 v-if="loged" >        
          <v-card color="blue-grey darken-2" class="white--text">
            <v-card-title primary-title>
              <v-layout wrap>              
                <v-flex xs12>
                  <v-text-field v-model="body" label="Post Something"></v-text-field>
                </v-flex> 
                
                <ul>
                  <li v-for="file in files">{{file.name}}</li>
                </ul>
                <file-upload
                    ref="upload"
                    v-model="files"
                    post-action="/post.method"
                    put-action="/put.method"
                    @input-file="inputFile"
                    @input-filter="inputFilter"
                >
                Upload file
                </file-upload>
                
              </v-layout>
            </v-card-title>
            <v-card-actions>
              <v-btn @click="publishPost" flat dark>Publish Post</v-btn>
            </v-card-actions>
          </v-card>
        </v-flex>

        <index-cards :canI="childState" v-on:increment="lockChild" ></index-cards>            
      </v-layout>
    </v-container>
  </div>

</template>

<script>
import FileUpload from 'vue-upload-component'
import indexCards from '~/components/IndexCards.vue'
// import fileUpload from '~/components/FileUpload2.vue'
import axios from 'axios'

export default {
  data () {
    return {
      body: '',
      childState: false,
      loged: false,
      files: []
    }
  },
  components: {
    indexCards,
    FileUpload
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
          // files: this.files
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
