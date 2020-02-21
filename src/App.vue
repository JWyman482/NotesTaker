<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-content>
      <v-app-bar app clipped-left>
        <v-toolbar-title class="green--text">NoteTaker</v-toolbar-title>
      </v-app-bar>

      <div class="" style="width: 500px; margin: auto;">
        <Note/>
      </div>

      <v-footer app>
          <span>&copy; 2019 - Layout Components from Vuetify</span>
      </v-footer>

    </v-content>
  </v-app>
</template>

<script>
import Note from "./components/Note.vue"

export default {
  name: 'App',

  components: {
    Note
  },

  data: () => ({
    //
  }),
};
</script>
