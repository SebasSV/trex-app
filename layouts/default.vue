<template>
  <v-app>

    <!-- Navigation bbar left side -->
    <v-navigation-drawer persistent :mini-variant="!miniVariant" :clipped="!clipped" v-model="drawer" app>
      <v-list>
        <v-list-tile  router :to="item.to" :key="i" v-for="(item, i) in items" exact>
          <v-list-tile-action>
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

      <v-btn>Language</v-btn>
      <v-btn>Loggin</v-btn>
      <fb-loggin></fb-loggin>


    </v-toolbar>

    <!-- Main nuxtPages -->
    <main>
      <v-content>
        <v-container>
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
import fbLoggin from '~/components/fbLoggin.vue'

export default {
  components: {
    fbLoggin
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
