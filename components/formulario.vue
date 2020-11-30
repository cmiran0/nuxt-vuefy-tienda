<template>
  <div>
    <v-container>
      <v-row>
        <v-text-field v-model="name" label="Producto nuevo" hide-details="auto"></v-text-field>
        <v-text-field v-model="descripcion" label="Descripción" hide-details="auto"></v-text-field>
        <v-text-field v-model="importe" label="Importe" hide-details="auto"></v-text-field>
        <v-text-field v-model="pvp" label="PVP" hide-details="auto"></v-text-field>
        <v-text-field v-model="impuesto" label="Imp." hide-details="auto"></v-text-field>
      </v-row>
    </v-container>
    <v-container>
      <v-row>
        <v-btn @click="addItem"> ADD</v-btn>
      </v-row>
    </v-container>

  </div>
</template>

<script>
export default {
  name: "formulario",
  data() {
    return {
      id: 0,
      name: null,
      descripcion: null,
      importe: 0,
      pvp: null,
      impuesto: 0

    }
  },
  methods: {
    addItem() {

      let item = {}
      item.id = ++this.id + 'pr'
      item.name = this.name
      item.descripcion = this.descripcion
      item.importe = this.importe
      item.pvp = this.pvp
      item.impuesto = this.impuesto


      this.$emit('subir-producto', item)


      this.name = null
      this.pvp = null

    }

  }

}


</script>

<style scoped>

</style>
