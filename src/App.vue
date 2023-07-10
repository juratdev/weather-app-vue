<script>
  import axios from 'axios';
  export default {
    data() {
      return {
        appKey: "04ec129461449c3117baadcc5c000d3b",
        query: "",
        urlBase: "https://api.openweathermap.org/data/2.5/",
        weather: {}
      }
    },
    methods: {
      fetchData() {
        axios.get(`${this.urlBase}/weather?q=${this.query}&units=metric&appid=${this.appKey}`)
          .then(res => this.weather = res)
        this.query = ""
      }
    }

  }
</script>

<template>
  <div class="w-full h-screen bg-gradient-to-r from-cyan-500 to-blue-500">
    <div class="container items-center w-1/3 px-8 py-8 pt-8 mx-auto">
      <div class="flex items-center justify-center space-x-2">
        <h1 class="px-1 text-4xl font-bold text-white rounded shadow">Weather App</h1>
        <img src="../public/images/icons8-weather.svg" alt="weather-icon">
      </div>
      <div class="flex w-full mt-9">
        <input
          class="w-full px-3 py-2 leading-tight text-gray-700 rounded-l-lg shadow appearance-none focus:outline-none focus:shadow-outline"
          type="text" placeholder="Enter a location" v-model="query" @keyup.enter="fetchData">
        <button class="px-3 py-2 font-semibold text-black bg-gray-200 rounded-r-lg shadow hover:bg-gray-300"
          @click="fetchData">Check</button>
      </div>
      <div v-if="(typeof weather.data != 'undefined')" class="mt-8 text-white">
        <h2 class="text-3xl font-bold">{{ weather.data.name }}, <span
            class="text-lg">{{ weather.data.sys.country }}</span></h2>
        <div class="flex items-center">
          <h3 class="mt-2 text-4xl font-bold">{{ Math.floor(weather.data.main.temp) }} °C</h3>
          <p class="pt-3 ps-6">{{weather.data.weather[0].main}}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>