<template>
  <v-app>
    <v-navigation-drawer app disable-route-watcher v-model="drawer">
      <v-toolbar flat>
        <v-list>
          <v-list-tile>
            <v-list-tile-title class="title">
              Menu
            </v-list-tile-title>
          </v-list-tile>
        </v-list>
      </v-toolbar>
      <v-divider></v-divider>
      <v-list dense class="pt-0">
        <v-list-tile v-for="item in items" :key="item.title" @click="move(item)">
          <v-list-tile-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>{{ item.title }}</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar app>
      <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
    </v-toolbar>
    <v-content class="main-content">
      <router-view></router-view>
    </v-content>
    <!-- <v-footer app></v-footer> -->
  </v-app>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      items: [
        { title: 'Home', icon: 'dashboard', href: 'main' },
        { title: 'About', icon: 'description', href: 'about' },
        { title: 'Photo', icon: 'linked_camera', href: 'photo' },
        { title: 'Map', icon: 'directions_car', href: 'map' }
      ],
      right: null,
      drawer: null
    }
  },
  methods: {
    move (item) {
      // if (item.href === 'main') {
      //   let container = document.getElementById('app')
      //   container.scrollTop = 0
      // }
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.main-content {
}
</style>
