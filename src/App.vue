<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="title">
        Backgammon NG
      </div>

      <v-spacer />
    </v-app-bar>

    <v-content>
      <router-view />
    </v-content>
  </v-app>
</template>

<script>
export default {
  name: 'App',
  data: () => ({}),
}
</script>
