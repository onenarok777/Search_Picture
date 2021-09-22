<template>
  <v-app dark>
    <v-app-bar fixed app>
      <v-list-item>
        <v-list-item-action>
          <v-btn text>Home</v-btn>
        </v-list-item-action>
      </v-list-item>
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data() {
    return {};
  },
};
</script>
