<template>

  <v-container>

    <v-row>
      <v-col>
        <formulario @subir-producto='addItem'></formulario>
      </v-col>
    </v-row>

    <v-row>
      <v-col cols="12" sm="6">
        <lista-productos :items="items" @subir-producto-ticket='addTicket'
                         @borrar-producto-ticket='delTicket'></lista-productos>
      </v-col>
      <v-col cols="12" sm="6">
        <lista-ticket :detallado="detallado" :ticket="ticket"></lista-ticket>
        <v-checkbox v-model="detallado" :label="detallado?'detallado':'no detallado'"></v-checkbox>
      </v-col>

    </v-row>


  </v-container>


</template>

<script>

import Formulario from "~/components/formulario";
import ListaProductos from "~/components/lista-productos";
import ListaTicket from "~/components/lista-ticket";


export default {
  components: {ListaTicket, ListaProductos, Formulario},

  computed: {
    ticket() {
      if (this.detallado) {
        return this.ticketDetallado
      }
      return this.ticketNoDetallado

    }

  },
  mounted() {
    this.$axios.get('/productos')
      .then(response => (
        this.items = response.data
      ))

  },
  data() {
    return {
      detallado: false,
      items: null,
      ticketDetallado: [],
      ticketNoDetallado: []

    }
  },
  methods: {
    addItem(item) {
      this.$axios.post('/productos', item).then(
        response => {
          this.items.push(item)
        }
      )


    },

    addTicket(item) {
      // detallado
      item.total = item.pvp
      item.cantidad = 1
      this.ticketDetallado.push(item)
      // no detallado
      let salir = false
      this.ticketNoDetallado.forEach((i) => {
        if (item.id === i.id) {
          i.cantidad = i.cantidad + 1
          i.total = (i.pvp * i.cantidad).toFixed(2)
          salir = true
        }
      })
      if (!salir) {
        let itemTicket = {}
        itemTicket.cantidad = 1
        itemTicket.name = item.name
        itemTicket.pvp = item.pvp
        itemTicket.id = item.id
        itemTicket.impuesto = item.impuesto
        itemTicket.total = item.pvp
        this.ticketNoDetallado.push(itemTicket)
      }

    },

    delTicket(item) {
      //detallado
      this.ticketDetallado.forEach((it, index) => {
        if (it === item) {
          this.ticketDetallado.splice(index, 1)

        }
      })
      //no detallado
      this.ticketNoDetallado.forEach((i, index) => {
        if (item.id === i.id && i.cantidad > 0) {
          i.cantidad = i.cantidad - 1
          i.total = i.pvp * i.cantidad
        }
        if (i.cantidad === 0) {
          this.ticketNoDetallado.splice(index, 1)
        }
      })
    },

  }
}
</script>
