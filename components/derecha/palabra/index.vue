<template>
  <v-container>
    <v-row>
      <v-col>
       <span v-for="(item, index) in items" :key="index">
           <v-chip class="ma-2">
             {{ item.Text }}
           </v-chip>
        </span>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "index",
  mounted() {
    this.$axios.get('/textractWord')
      .then(response => (
        this.items = response.data
      ))
  },
  data() {
    return {
      items: null
    }
  },
  methods: {}
}
</script>

<style scoped>

</style>
