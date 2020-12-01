<template>


  <div>

      <v-card class="mx-auto" tile>
        <v-card-title>LISTA PRODUCTOS</v-card-title>
        <v-card-subtitle>* imp incluidos</v-card-subtitle>
        <v-list dense>
          <v-list-item-group color="primary">
            <v-list-item v-for="item in items">
              <v-list-item-content>
                <v-list-item-title v-html="item.name"></v-list-item-title>
                <v-list-item-subtitle v-html="item.descripcion"></v-list-item-subtitle>
                <v-list-item-subtitle v-html="item.pvp"></v-list-item-subtitle>
              </v-list-item-content>
              <v-btn @click="addTicket(item)">+</v-btn>
              <v-btn @click="delTicket(item)">-</v-btn>
            </v-list-item>
          </v-list-item-group>
        </v-list>
      </v-card>


  </div>


</template>

<script>
export default {
  name: "lista-productos",
  props: ['items'],
  data: function () {
    return {
      id: 5,
      name: null,
      pvp: null,
    }
  },
  methods: {
    addTicket(item) {
      this.$emit('subir-producto-ticket', item)
    },
    delTicket(item) {
      this.$emit('borrar-producto-ticket', item)
    }
  }
}
</script>
