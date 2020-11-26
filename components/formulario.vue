<template>
  <div>
    <v-text-field
      v-model="name"
      label="Producto nuevo"
      hide-details="auto"
    ></v-text-field>
    <v-text-field v-model="pvp" label="Importe"></v-text-field>

    <v-btn @click="addItem"> ADD</v-btn>


  </div>
</template>

<script>
export default {
  name: "formulario",
  data() {
    return {
      id: 0,
      name: null,
      pvp: null

    }
  },
  methods: {
    addItem() {
      let item = {}
      item.name = this.name
      item.pvp = this.pvp
      item.id = ++this.id + 'pr'

      this.$emit('subir-producto', item)
      this.name = null
      this.pvp = null

    }

  }

}


</script>

<style scoped>

</style>
