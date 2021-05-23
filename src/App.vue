<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-icon>mdi-menu</v-icon>
      </div>

      <v-spacer></v-spacer>

      <v-icon>mdi-bell-check</v-icon>
    </v-app-bar>

    <v-main>
      <ItemsList/>
    </v-main>
  </v-app>
</template>

<script>
import ItemsList from './components/items/item.list';

export default {
  name: 'App',

  components: {
    ItemsList,
  },

  data: () => ({
    //
  }),
};
</script>
