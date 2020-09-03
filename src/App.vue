<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <h2>Where's Covid: An Interactive Map</h2>
    </v-app-bar>

    <v-main>
      <Home />
    </v-main>
  </v-app>
</template>

<script>
import Home from "@/components/Home";

export default {
  name: "App",

  components: {
    Home
  },

  data: () => ({
    //
  })
};
</script>
