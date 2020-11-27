<template>
  <div>
    <formulario @subir-producto='addItem'></formulario>
    <lista-productos :items="items" @subir-producto-ticket='addTicket'
                     @borrar-producto-ticket='delTicket'></lista-productos>
    <v-checkbox
      v-model="detallado"
      :label="detallado?'detallado':'no detallada'"
    ></v-checkbox>
    <lista-ticket :detallado="detallado" :ticket="ticket"></lista-ticket>
  </div>
</template>

<script>

import Formulario from "~/components/formulario";
import ListaProductos from "~/components/lista-productos";
import ListaTicket from "~/components/lista-ticket";

export default {
  components: {ListaTicket, ListaProductos, Formulario},
  data() {
    return {
      detallado: false,
      items: [{id: 1, name: 'manzana', pvp: 10},
        {id: 2, name: 'pera', pvp: 8}],
      ticket: []
    }
  },
  methods: {
    addItem(item) {
      this.items.push(item)
    },
    addTicketTipoDetallado(item) {
      item.total = item.pvp
      this.ticket.push(item)
    },
    addTicketTipoNoDetallado(item) {
      let salir = false
      this.ticket.forEach((i) => {
        if (item.id === i.id) {
          console.log("++Hay un objeto " + i.name)
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
        console.log("Crea objeto " + itemTicket.name)

        this.ticket.push(itemTicket)
      }
    },
    addTicket(item) {
      if (this.detallado) {
        this.addTicketTipoDetallado(item)
        return false
      }
      this.addTicketTipoNoDetallado(item)
    },
    delTicket(item) {
      if (this.detallado) {
        this.delTicketTipoDetallado(item)
        return false
      }
      this.delTicketTipoNoDetallado(item)
    },
    delTicketTipoNoDetallado(item) {
      this.ticket.forEach((i, index) => {
        if (item.id === i.id && i.cantidad > 0) {
          i.cantidad = i.cantidad - 1
          i.total = i.pvp * i.cantidad
        }
        if (i.cantidad === 0) {
          this.ticket.splice(index, 1)
        }
      })

    },
    delTicketTipoDetallado(item) {
      let salir = false
      this.ticket.forEach((it, index) => {
        if (!salir) {
          if (it === item) {
            this.ticket.splice(index, 1)
            salir = true
          }
        }
      })
    }
  }
}
</script>
