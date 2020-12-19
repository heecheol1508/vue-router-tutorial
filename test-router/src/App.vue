<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app>
      <v-list dense>
        <v-list-item router :to="{ name: 'Home' }" exact>
          <v-list-item-icon>
            <v-icon>{{ "mdi-view-dashboard" }}</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title>Home</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-list-item router :to="{ name: 'About' }" exact>
          <v-list-item-icon>
            <v-icon>{{ "mdi-forum" }}</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title>About</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-list-item
          router
          :to="{
            name: 'Users',
            params: {
              userId: 'heecheol',
            },
            query: {
              group: 'member',
              category: 'trial',
            },
          }"
          exact
        >
          <v-list-item-icon>
            <v-icon>{{ "mdi-account-group-outline" }}</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title>Users</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>Application</v-toolbar-title>
    </v-app-bar>

    <v-main class="ma-5">
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      drawer: null,
      items: [
        { title: "Home", icon: "mdi-view-dashboard", name: "Home" },
        { title: "About", icon: "mdi-forum", name: "About" },
        { title: "Users", icon: "mdi-account-group-outline", name: "Users" },
      ],
      right: null,
    };
  },
};
</script>