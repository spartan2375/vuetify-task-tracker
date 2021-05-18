<template>
  <v-app id="inspire">
    <v-navigation-drawer 
      v-model="drawer" 
      app
      >

      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="title"> Task Tracker </v-list-item-title>
          <v-list-item-subtitle> simple stuff </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list 
      dense 
      nav
      >
        <v-list-item
         v-for="item in items" 
         :key="item.title" 
         :to="item.to" 
         link
         >

          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      app
      dark
      color="primary"
      prominent
      src="waves.jpg"
    >
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>Vuetify Task Tracker</v-toolbar-title>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    drawer: null,
    items: [
      { title: "Tasks", icon: "mdi-text-box-check-outline", to: "/" },
      { title: "About", icon: "mdi-help", to: "/about" },
    ],
  }),
}
</script>