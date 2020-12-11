<template>
  <v-container>
    <v-row>
      <v-col>
        <izquierda></izquierda>
      </v-col>
      <v-col>
        <derecha></derecha>
      </v-col>
    </v-row>


  </v-container>

</template>

<script>
import Derecha from "../../components/derecha";
import Izquierda from "../../components/izquierda";

export default {
  name: "index",
  components: {Izquierda, Derecha}
}
</script>

<style scoped>

</style>
