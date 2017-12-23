<template>
  <v-app>

    <!-- Navigation bbar left side -->
    <v-navigation-drawer persistent :mini-variant="!miniVariant" :clipped="!clipped" v-model="drawer" app>
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
      <v-btn  icon @click.stop="miniVariant = !miniVariant" >
        <v-icon v-html="miniVariant ? 'chevron_right' : 'chevron_left'"></v-icon>
      </v-btn>

      <v-toolbar-title v-text="title"></v-toolbar-title>

      <v-spacer></v-spacer>

      <dialog-login v-if="!loged"></dialog-login>
      <v-btn v-if="!loged">Facebook</v-btn>
      <user-interface></user-interface>
      <!-- <a href="http://localhost:8080/login">Facebook</a> -->


    </v-toolbar>

    <!-- Main nuxtPages -->
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
import dialogLogin from '~/components/DialogLogin.vue'
import UserInterface from '~/components/UserInterface.vue'
export default {
  data () {
    return {
      clipped: false,
      drawer: true,
      fixed: false,
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: '3A',
      loged: false,
      items: [
        { icon: 'apps', title: 'Welcome', to: '/', can: true },
        { icon: 'bubble_chart', title: 'Inspire', to: '/inspire', can: true }
      ]
    }
  },
  components: {
    dialogLogin,
    UserInterface
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
