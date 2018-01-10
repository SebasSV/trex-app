<template>
  <v-app>

    <!-- Navigation bbar left side -->
      <v-navigation-drawer v-if="loged" persistent :mini-variant="!miniVariant" :clipped="!clipped" v-model="drawer" app>
        <v-list>
          <v-list-tile router :to="item.to" :key="i" v-for="(item, i) in items" exact>
           <v-list-tile-action v-if="item.can">
              <v-icon v-html="item.icon"></v-icon>
            </v-list-tile-action>
            <v-list-tile-content>
             <v-list-tile-title v-text="item.title"></v-list-tile-title>
           </v-list-tile-content>
         </v-list-tile>
       </v-list>
     </v-navigation-drawer>

    <!-- Header toolBar -->
    <v-toolbar fixed app :clipped-left="!clipped">      

        <v-flex xs2>
          <v-toolbar-title v-text="title"></v-toolbar-title>
        </v-flex>  
      
        <v-flex xs3>                                            
          <b-input-group md="4" size="sm" class="mb-3">              
            <b-form-input type="text" />             
            <b-input-group-addon @click="searchPost" style="cursor: pointer"><v-icon>search</v-icon></b-input-group-addon>
          </b-input-group>             
        </v-flex>  
      
        <v-spacer></v-spacer>      
        <user-interface v-on:logout="loged = false"></user-interface>                            

    </v-toolbar>

    <main>
      <v-content>
        <v-container grid-list-md text-xs-center fluid>
          <nuxt />
        </v-container>
      </v-content>
    </main>

    <!-- Footer -->
    <v-footer :fixed="!fixed" app>
      <span>&copy; 2017</span>
    </v-footer>

  </v-app>
</template>

<script>
import UserInterface from '~/components/UserInterface.vue'
import dialogLogin from '~/components/DialogLogin.vue'
import axios from 'axios'
export default {
  data () {
    return {
      drawer: true,
      clipped: false,
      fixed: false,
      title: '3A',
      loged: false,
      miniVariant: false,
      items: [
        { icon: 'apps', title: 'Welcome', to: '/', can: true },
        { icon: 'bubble_chart', title: 'Inspire', to: '/inspire', can: true }
      ]
    }
  },
  components: {
    UserInterface,
    dialogLogin
  },
  mounted () {
    this.loadUserOptions()
  },
  methods: {
    loadUserOptions () {
      if (this.getCookie('access_token')) {
        this.loged = true
      }
      axios({
        method: 'get',
        url: 'http://localhost:8080/user',
        headers: {'Content-Type': 'application/json'}
      }).then(function (response) {
        if (response) {
          return 'some'
        }
      })
    },
    getCookie (name) {
      var value = '; ' + document.cookie
      var parts = value.split('; ' + name + '=')
      if (parts.length === 2) return parts.pop().split(';').shift()
    },
    searchPost () {
      axios({
        method: 'get',
        url: 'http://localhost:8080/getUsername',
        headers: {'Content-Type': 'application/json'},
        params: {
          access_token: this.getCookie('access_token')
        }
      }).then(function (response) {
        if (response) {
          this.loged = false
          this.$emit('logout')
          this.delete_cookie('access_token')
          this.$router.go('/')
        }
      }.bind(this))
    }
  }
}
</script>
