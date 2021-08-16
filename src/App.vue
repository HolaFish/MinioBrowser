<template>
  <v-app>
    <v-system-bar app>
      <v-icon color="blue">mdi-web-box</v-icon>
      <span>Minio Browser</span>
      <v-spacer></v-spacer>
      <v-icon>mdi-minus</v-icon>
      <v-icon>mdi-checkbox-blank-outline</v-icon>
      <v-icon>mdi-close</v-icon>
    </v-system-bar>
    <v-navigation-drawer app>
      <buckets-list></buckets-list>
    </v-navigation-drawer>
    <v-main>
      abc
    </v-main>
  </v-app>
</template>

<script>
import BucketsList from './components/BucketsList.vue';

export default {
  name: 'App',
  components: {
    BucketsList,
  },

  data: () => ({
    //
  }),
};
</script>
