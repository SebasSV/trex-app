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

      <v-toolbar-title v-text="title"></v-toolbar-title>

      <v-spacer></v-spacer>      
      <user-interface v-on:logout="loged = false"></user-interface>
      
      <!-- <a href="http://localhost:8080/login">Facebook</a> -->


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
    },
    getCookie (name) {
      var value = '; ' + document.cookie
      var parts = value.split('; ' + name + '=')
      if (parts.length === 2) return parts.pop().split(';').shift()
    }
  }
}
</script>
