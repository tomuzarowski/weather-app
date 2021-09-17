<template>
  <form @submit.prevent="getData">
    <label for="city">Please, enter a city name</label>
    <input type="text" id="city" v-model="city">
    <p class="error" v-if="cityNotFoundError">Sorry, "{{cityNotFoundName}}" was not found :(</p>

    <img src="../assets/weather.svg" alt="Weather Icon">
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
      const url = `//api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=${process.env.VUE_APP_API_KEY}`;
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
form {
  align-items: center;
  display: flex;
  flex-direction: column;
  /*position: relative;*/
}

form label {
  color: var(--orange);
  font-weight: bold;
  margin-bottom: 1em;
  text-align: center;
  width: 100%;
}

form input {
  background-color: var(--gray);
  border: none;
  border-radius: 8px;
  box-shadow: 0 8px 20px rgba(0,0,0, .3);
  color: var(--blue);
  font-size: 2.4rem;
  outline: none;
  text-align: center;
  padding: 1em 0;
}

img {
  height: auto;
  opacity: .05;
  position: absolute;
  left: 45vw;
  top: 30vh;
  /*transform: translateY(-50%);*/
  width: 30vw;
  z-index: -1;
}

.error {
  background-color: var(--orange);
  color: var(--blue);
  margin-top: 1rem;
  padding: 1rem;
}

@media (min-width: 400px) {
  img {
    top: 20vh;
  }
}

</style>