<template>
  <form @submit.prevent="getData">
    <label for="city">Please, enter a city name</label>
    <input @input="getData" type="text" id="city" v-model="city">
  </form>
</template>

<script>
export default {
  data() {
    return {
      city: ""
    }
  },
  methods: {
    getData() {
      if (this.city.length > 2) {
        console.log(this.city);
      }
    }
  },
  name: "Form"
}
</script>

<style scoped>

</style>