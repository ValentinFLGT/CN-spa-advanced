<template>
  <div>
    <h1>Carte des villes</h1>
  </div>
</template>

<script lang="ts">
import axios from "axios";

export default class CitiesMap {

  cities: Array<string> = []

  loadCities(citiesData: Array<string>) {
    this.cities = [];
    for (const {
      name,
      coord: {lat, lon},
      weather: [{description: weather, icon: icon}],
      main: {temp: temperature},
      dt: updatedAt
    } of citiesData) {
      this.cities.push({name, lat, lon, weather, icon, temperature, updatedAt: new Date(updatedAt * 1000)});
    }
  }

  mounted() {
    axios.get(`https://api.openweathermap.org/data/2.5/find?lat=${process.env.VUE_APP_DEFAULT_LATITUDE}&lon=${process.env.VUE_APP_DEFAULT_LONGITUDE}&cnt=20&cluster=yes&lang=fr&units=metric&APPID=${process.env.VUE_APP_OW_APP_ID}`)
        .then((resp) => this.loadCities(resp.data.list));
  }

}
</script>

<style scoped>
h1 {
  margin: 40px 0 0;
}

</style>
