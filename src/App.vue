<template>
  <v-app id="nomnom">
    <v-navigation-drawer
      disable-resize-watcher
      color="primary"
      v-model="drawer"
      fixed
      right
      app
    >
      <v-list dense>
        <v-list-tile @click="$router.push('/')">
          <v-list-tile-action>
            <v-icon>home</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>Home</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile @click="$router.push('/create')">
          <v-list-tile-action>
            <v-icon>add_circle</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>New Room</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile @click="$router.push('/help')">
          <v-list-tile-action>
            <v-icon>help</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>Help</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar color="primary" dark fixed flat app>
      <v-toolbar-title>NomNominate</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items>
        <ul>
          <li v-for="user in users">{{ user.name }}</li>
        </ul>
        <v-toolbar-side-icon @click.stop="drawer = !drawer" class="hidden-sm-and-up"></v-toolbar-side-icon>
        <v-btn flat class="hidden-xs-only" @click="$router.push('/create')"><v-icon>add_circle</v-icon> New Room</v-btn>
        <v-btn flat class="hidden-xs-only" @click="$router.push('/help')"><v-icon>help</v-icon> Help</v-btn>
        <v-btn flat class="hidden-xs-only" @click="$router.push('/')"><v-icon>home</v-icon> Home</v-btn>
      </v-toolbar-items>
    </v-toolbar>
    <v-content>
      <v-container fluid fill-height class="nopad">
        <v-layout
          justify-center
        >
          <v-flex text-xs-center>
            <router-view></router-view>
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
const config = {
  headers: {'Authorization': 'qcynQs_bSkqkZdzR9S4lCn3p0dGyFSFJ5BDtfvNzB8wd5y7pqhr69Zt6Bj8YwfK6BAr9KYc1L55U-fmsUUGyHxBqXzOqFpLpHSeotKafcccOGQBIVL0PuDBiuKCOXHYx'},
  params: {
    term: 'tacos',
    location: 'main 123st'
  }
};
export default {
  data: () => ({
    drawer: false,
    users: [],
  }),
  created () {
    var vm = this
    axios.get('https://api.yelp.com/v3/businesses/search', config)
      .then(function (response) {
        vm.users = response.data
      })},
  props: {
    source: String,
  },
};
</script>

  

<style>
@import './assets/main.css';
</style>
