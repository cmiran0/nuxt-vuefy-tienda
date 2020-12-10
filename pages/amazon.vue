<template>
  <v-container>
    <v-row>
      <v-col cols="12" sm="6">
        <v-btn>btn</v-btn>
      </v-col>
      <v-col cols="12" sm="6">
        <lista-amazon></lista-amazon>
      </v-col>

    </v-row>
  </v-container>
</template>

<script>


import ListaAmazon from "../components/lista-amazon";
export default {

  name: "amazon",
  components: {ListaAmazon}
}
</script>

<style scoped>

</style>
