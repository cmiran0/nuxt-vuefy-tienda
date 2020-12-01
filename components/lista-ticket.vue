<template>
  <div>
    <v-card>
      <v-card-title>CARRITO {{ detallado ? " DETALLADO" : " NO DETALLADO" }}</v-card-title>
      <v-list>
        <v-list-item-group color="primary">
          <v-list-item v-for="(item, i) in ticket" :key="i">
            <v-list-item-content>
              <v-col>
                <v-list-item-title v-text="item.name"></v-list-item-title>
                <v-list-item-subtitle v-text="'pvp: '+item.pvp"></v-list-item-subtitle>
              </v-col>
              <v-col>
                <v-list-item-title v-text="'cant: '+item.cantidad" v-if="!detallado"></v-list-item-title>
                <v-list-item-subtitle v-text="'total: '+item.total" v-if="!detallado"></v-list-item-subtitle>
              </v-col>
            </v-list-item-content>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-card>
    <v-list-item-content>
      <v-col>
        <v-list-item-subtitle v-text="'Sin Imp: '"></v-list-item-subtitle>
        <v-list-item-subtitle v-text="'Imp Incluidos'"></v-list-item-subtitle>
      </v-col>
      <v-col>
        <v-list-item-subtitle v-text="impNoIcluidos"></v-list-item-subtitle>
        <v-list-item-subtitle v-text="total"></v-list-item-subtitle>
      </v-col>


    </v-list-item-content>
    <v-btn @click="pagar()">TOTAL:{{ total }}</v-btn>
  </div>
</template>

<script>
export default {
  name: "lista-ticket",
  props: ['ticket', 'detallado'],
  computed: {
    total() {
      let total = 0
      this.ticket.forEach((item) => {

        total += parseFloat(item.total)
      })
      return total
    },
    impNoIcluidos() {
      let suma = 0
      this.ticket.forEach((item) => {
        let imp = parseFloat(item.impuesto)
        let total = parseFloat(item.total)
        suma += total - (total * imp / 100)
      })
      return suma
    },
  },
  methods: {
    pagar() {
      alert('Tienes que pagar ' + this.total + ' .eur')
    }
  }
}
</script>

<style scoped>
</style>
