<template>
  <div>
    <v-navigation-drawer v-model="drawer" absolute temporary app
      class="lighten-2"
      disable-resize-watcher>
      <v-img :aspect-ratio="18/9" src="https://cdn.vuetifyjs.com/images/parallax/material2.jpg">
      <v-container class="pa-1">
        <v-card>
          <v-img :src="user().photoURL"
            class="white--text" height="150px">
            <v-card-title
              class="fill-height align-end"
              v-text="user().displayName"
            ></v-card-title>
          </v-img>

          <v-card-actions>
            <div class="flex-grow-1"></div>
            <v-btn icon to="/user/profile"> <v-icon>mdi-account</v-icon> </v-btn>
            <v-btn icon to="/user/form"> <v-icon>mdi-account-edit</v-icon> </v-btn>
          </v-card-actions>
        </v-card>
      </v-container>
      </v-img>

      <v-divider></v-divider>

      <v-list dense>
        <v-list-item v-for="item in items" :key="item.title" link :to="item.url">
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
      <template v-slot:append>
        <div class="pa-2">
          <v-btn block @click.stop="logout">Logout</v-btn>
        </div>
      </template>
    </v-navigation-drawer>

    <v-app-bar app color="deep-purple accent-4" dense dark collapse collapse-on-scroll>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>Page title</v-toolbar-title>

      <div class="flex-grow-1"></div>

      <v-btn icon>
        <v-icon>mdi-heart</v-icon>
      </v-btn>

      <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>

      <v-menu transition="slide-y-transition" bottom>
        <template v-slot:activator="{ on }">
          <v-btn icon v-on="on">
            <v-icon>mdi-dots-vertical</v-icon>
          </v-btn>
        </template>

        <v-list>
          <v-list-item v-for="n in 5" :key="n" @click="() => {}">
            <v-list-item-title>
              <v-icon>mdi-account-arrow-right</v-icon>
              Option {{ n }}
            </v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>
  </div>
</template>

<script>
export default {
  name: 'AppNavigation',
  data () {
    return {
      drawer: false,
      group: null,
      items: [
        {
          title: 'Home',
          url: '/',
          icon: 'mdi-home'
        },
        {
          title: 'About',
          url: '/about',
          icon: 'mdi-heart'
        }
      ]
    }
  },
  computed: {
    isAuthenticated () {
      return this.$store.getters.isAuthenticated
    }
  },
  watch: {
    group () {
      this.drawer = false
    }
  },
  methods: {
    logout () {
      this.$store.dispatch('userSignOut')
    },
    user () {
      return this.$store.state.user
    }
  }
}
</script>

<style scoped>
</style>
