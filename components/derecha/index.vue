<template>
  <v-container>

    <v-tabs v-model="tab" align-with-title>
      <v-tabs-slider color="white"></v-tabs-slider>
      <v-tab v-for="item in items" :key="item">
        {{ item }}
      </v-tab>
    </v-tabs>

    <v-tabs-items v-model="tab">
      <v-tab-item>
        <linea></linea>
      </v-tab-item>
      <v-tab-item>
        <palabra></palabra>
      </v-tab-item>
    </v-tabs-items>
  </v-container>
</template>

<script>
import Linea from "./linea";
import Palabra from "./palabra";

export default {
  name: "derecha",
  components: {Linea, Palabra},
  data() {
    return {
      items: ['lista', 'palabra'],
      tab: null,
      text: 'hola'
    }
  }
}
</script>

<style scoped>

</style>
