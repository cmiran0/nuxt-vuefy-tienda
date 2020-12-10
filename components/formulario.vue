<template>

  <v-form v-model="valid">
    <v-container>
      <v-row>
        <v-col cols="12" md="4">
          <v-text-field
            v-model="name"

            :counter="10"
            label="Nombre"
            required
          ></v-text-field>
        </v-col>

        <v-col cols="12" md="4">
          <v-text-field
            v-model="descripcion"

            :counter="10"
            label="Descripción"
            required
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="4">
          <v-text-field
            v-model="pvp"

            :counter="10"
            label="pvp"
            required
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="4">
          <v-text-field
            v-model="impuesto"

            :counter="10"
            label="Imp."
            required
          ></v-text-field>
        </v-col>

        <v-col cols="12" md="4">
          <v-btn @click="addItem"> ADD</v-btn>
        </v-col>
      </v-row>

    </v-container>
  </v-form>


</template>

<script>
export default {
  name: "formulario",
  data() {
    return {
      valid: true,
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

      if (this.valid) {
        this.$emit('subir-producto', item)
      }


      this.name = null
      this.pvp = null
      this.descripcion = null
      this.impuesto = null
    }

  }

}


</script>

<style scoped>

</style>
