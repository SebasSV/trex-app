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

        <index-cards></index-cards>
        

      </v-layout>
    </v-container>
  </div>
</template>

<script>
import indexCards from '~/pages/indexCards.vue'

export default {
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
  },
  components: {
    indexCards
  }
}
</script>
