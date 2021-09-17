<template>
  <form @submit.prevent="getData">
    <label for="city">Please, enter a city name</label>
    <input type="text" id="city" v-model="city">
    <p class="error" v-if="cityNotFoundError">Sorry, "{{cityNotFoundName}}" was not found :(</p>
  </form>
</template>

<script>
export default {
  data() {
    return {
      city: "",
      cityNotFoundName: "",
      cityNotFoundError: false
    }
  },
  methods: {
    getData: function () {
      const key = "db17ba294ac990b1d000281bf33e1951";
      const url = `//api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=${key}`;
      fetch(url)
          .then(response => response.json())
          .then(data => {
            if (data.message === "city not found") {
              this.cityNotFoundError = true;
              this.cityNotFoundName = this.city;
              this.city = "";
            } else {
              console.log(data);
              this.cityNotFoundError = false;
              this.cityNotFoundName = "";
            }
          });
    }
  },
  name: "Form"
}
</script>

<style scoped>
.error {
  background-color: var(--orange);
  color: var(--blue);
  margin-top: 1rem;
  padding: 1rem;
}
</style>