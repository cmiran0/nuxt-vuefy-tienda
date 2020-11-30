<template>
  <div>
    <formulario @subir-producto='addItem'></formulario>
    <lista-productos :items="items" @subir-producto-ticket='addTicket'
                     @borrar-producto-ticket='delTicket'></lista-productos>
    <v-checkbox v-model="detallado" :label="detallado?'detallado':'no detallada'"></v-checkbox>
    <lista-ticket :detallado="detallado" :ticket="ticket"></lista-ticket>


  </div>
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
  data() {
    return {
      detallado: false,
      items: [
        {id: 1, name: 'manzana', pvp: 5},
        {id: 2, name: 'pera', pvp: 10},
        {id: 3, name: 'tomate', pvp: 15},
        {id: 4, name: 'pepino', pvp: 12},
        {id: 5, name: 'piña', pvp: 13}],
      ticketDetallado: [],
      ticketNoDetallado: []
    }
  },
  methods: {
    addItem(item) {
      this.items.push(item)
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
          i.total = i.pvp * i.cantidad
          salir = true
        }
      })
      if (!salir) {
        let itemTicket = {}
        itemTicket.cantidad = 1
        itemTicket.name = item.name
        itemTicket.pvp = item.pvp
        itemTicket.id = item.id
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

