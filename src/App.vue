<template>
  <div class="app">
    <form class="search" @submit.prevent="fetchData">
      <input type="text" name="City" v-model="city" />
      <button type="submit">Search</button>
    </form>
    <main v-if="Object.keys(data).length !== 0">
      <div class="city-name">
        <h4>Weather in <br />{{ data.name }}, {{ data.sys.country }}</h4>
      </div>
      <div class="temperature">
        <h1>{{ data.main.temp.toFixed(0) }} °C</h1>
      </div>
    </main>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import axios from "axios";
import "dotenv/config";

export default defineComponent({
  name: "App",
  components: {},
  data() {
    return {
      city: "",
      data: {},
    };
  },
  methods: {
    async fetchData() {
      const { data } = await axios.get(
        process.env.API_KEY +
          this.city
      );
      this.data = data;
      console.log(this.data);
    },
  },
});
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap");

#app {
  display: flex;
  flex-direction: column;

  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  justify-content: center;
  align-items: center;
  text-align: center;

  background-color: rgb(107, 201, 255);

  height: 100vh;

  margin: 0px;
  padding: 0px;

  font-family: "Roboto", sans-serif;
}

.search input,
.search button {
  margin: 0px 5px;
}

main {
  padding: 70px 0px;
  color: white;
}

.city-name {
  margin: 20px;
  font-size: 20px;
}

.temperature {
  font-size: 100px;
}

.city-name,
.temperature {
  filter: drop-shadow(2px 2px 2px rgba(48, 48, 48, 0.466));
}
</style>
