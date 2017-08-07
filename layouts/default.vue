<style lang="stylus" scoped>

  .navigation-drawer
    background: url('https://source.unsplash.com/collection/477/300x1440') no-repeat
    padding: 0
    .tint
      background: linear-gradient(to bottom, rgba(255,255,255,.95) 0%,rgba(255,255,255,0.8) 100%); /* W3C, IE10+, FF16+, Chrome26+, Opera12+, Safari7+ */
      height: 100%
      padding: 0 0 100px

  .application--dark .navigation-drawer
    background: url('https://source.unsplash.com/collection/296884/300x1440') no-repeat
    .tint
      background: linear-gradient(to bottom, rgba(30,30,30,1) 0%,rgba(30,30,30,0.7) 100%); /* W3C, IE10+, FF16+, Chrome26+, Opera12+, Safari7+ */
      height: 100%
      padding: 0 0 100px

  .externalLinks
    position: absolute
    bottom: 1em
    width: 300px
</style>


<template>
  <v-app :dark="dark"
         toolbar
         footer>
    <v-navigation-drawer persistent
                         :mini-variant="miniVariant"
                         :clipped="clipped"
                         v-model="drawer">
  
      <div class="tint">
  
        <v-list>
          <v-list-tile router
                       v-for="(item, i) in items"
                       :to="item.to"
                       :key="i">
            <v-list-tile-action>
              <v-icon v-html="item.icon"></v-icon>
            </v-list-tile-action>
            <v-list-tile-content>
              <v-list-tile-title v-text="item.title"></v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
        </v-list>
  
        <v-list class="externalLinks">
          <template v-for="(item, i) in externalLinks">
            <v-list-tile :key="i"
                         :href="item.href"
                         target="_blank">
              <v-list-tile-action>
                <v-icon v-html="item.icon"></v-icon>
              </v-list-tile-action>
              <v-list-tile-content>
                <v-list-tile-title v-text="item.title"></v-list-tile-title>
              </v-list-tile-content>
            </v-list-tile>
          </template>
  
        </v-list>
      </div>
    </v-navigation-drawer>
    <v-toolbar fixed
               class="elevation-0">
      <v-toolbar-side-icon @click.native.stop="drawer = !drawer"></v-toolbar-side-icon>
      <v-btn icon
             @click.native.stop="miniVariant = !miniVariant">
        <v-icon v-html="miniVariant ? 'chevron_right' : 'chevron_left'"></v-icon>
      </v-btn>
      <v-toolbar-title>Chava Sobreyra</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn icon
             @click.native.stop="dark = !dark">
        <v-icon v-html="dark ? 'mdi-weather-night' : 'mdi-weather-sunny'"></v-icon>
      </v-btn>
    </v-toolbar>
    <main>
      <v-container fluid>
        <nuxt />
      </v-container>
    </main>
    <v-navigation-drawer temporary
                         :right="right"
                         v-model="rightDrawer">
      <v-list>
        <v-list-tile @click.native="right = !right">
          <v-list-tile-action>
            <v-icon light>compare_arrows</v-icon>
          </v-list-tile-action>
          <v-list-tile-title>Switch drawer (click me)</v-list-tile-title>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-footer>
      <span>&copy; 2017</span>
    </v-footer>
  </v-app>
</template>

<script>
  export default {
    computed: {
      dark() {
        const currentHour = new Date().getHours()
        return !(currentHour > 7 && currentHour < 21)
      }
    },
    data() {
      return {
        clipped: false,
        drawer: true,
        items: [
          { icon: 'apps', title: 'Welcome', to: '/' },
          { icon: 'mdi-view-carousel', title: 'Portfolio', to: '/portfolio' },
          { icon: 'mdi-file-document-box', title: 'Resume', to: '/resume' }
        ],
        externalLinks: [
          { icon: 'mdi-github-circle', title: 'GitHub', href: 'https//:github.com/ChavaSobreyra' },
          { icon: 'mdi-linkedin', title: 'LinkedIn', href: '/resume' },
          { icon: 'mdi-twitter', title: 'Twitter', href: '/resume' }
        ],
        miniVariant: false,
        right: true,
        rightDrawer: false,
        title: 'Vuetify.js'
      }
    }
  }
</script>
