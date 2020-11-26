<template>
  <div>
    <formulario @subir-producto='addItem'></formulario>
    <lista-productos :items="items" @subir-producto-ticket='addTicket'
                     @borrar-producto-ticket='delTicket'></lista-productos>
    <lista-ticket :ticket="ticket"></lista-ticket>
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
      items: [{id: 1, name: 'manzana', pvp: 10},
        {id: 2, name: 'peras', pvp: 8}],
      ticket: []
    }
  },
  methods: {
    addItem(item) {
      this.items.push(item)
    },
    addTicket(item) {
      this.ticket.push(item)
    },
    delTicket(item) {
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
