<template>
  <div>
    <br>
    <v-card
      class="mx-auto2"
      tile
    >
      <v-card-title>CARRITO</v-card-title>
      <v-list dense>
        <v-list-item-group color="primary">
          <v-list-item
            v-for="(item, i) in ticket"
            :key="i"
          >
            <v-list-item-content>
              <v-list-item-title v-text="item.name"></v-list-item-title>
              <v-list-item-subtitle v-text="item.pvp"></v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-card>
    <br>
    <v-btn @click="pagar()">TOTAL:{{ total }}</v-btn>
  </div>


</template>

<script>
export default {
  name: "lista-ticket",
  props: ['ticket'],
  computed: {
    total() {
      let total = 0
      this.ticket.forEach((item) => {
        total += parseInt(item.pvp)
      })
      return total
    }
  },
  methods: {
    pagar() {
      alert('Tienes que pagar '+this.total+' .eur')
    }
  }
}
</script>

<style scoped>

</style>
