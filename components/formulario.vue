<template>

  <div>
    <v-col>
      <v-row>
        <v-text-field v-model="name" label="Producto nuevo" hide-details="auto"></v-text-field>
        <v-text-field v-model="descripcion" label="Descripción" hide-details="auto"></v-text-field>
        <v-text-field v-model="pvp" label="pvp" hide-details="auto"></v-text-field>
        <v-text-field v-model="impuesto" label="Imp" hide-details="auto"></v-text-field>
      </v-row>
    </v-col>
    <v-col>
      <v-btn @click="addItem"> ADD</v-btn>
    </v-col>
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
      pvp: null,
      impuesto: null

    }
  },
  methods: {
    addItem() {
      let item = {}
      item.id = ++this.id + 'pr'
      item.name = this.name
      item.descripcion = this.descripcion
      item.impuesto = this.impuesto
      item.pvp = parseFloat(this.pvp) + parseFloat((this.pvp * this.impuesto / 100))


      this.$emit('subir-producto', item)


      this.name = null
      this.pvp = null
      this.descripcion = null
      this.importe = null
      this.impuesto = null

    }

  }

}


</script>

<style scoped>

</style>
