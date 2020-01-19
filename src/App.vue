<template>
  <div id="app">
    <h1>Earthquake Tracker</h1>
    <large-earthquake-list v-bind:largeEarthquakes="largeEarthquakes" />
  </div>
</template>

<script>
import {eventBus} from './main.js';
import LargeEarthquakeList from './components/LargeEarthquakeList.vue';

export default {
  name: 'app',
  components: {
    "large-earthquake-list": LargeEarthquakeList
  },
  data(){
    return {
      largeEarthquakes: []
    };
  },
  mounted() {
    fetch('https://earthquake.usgs.gov/fdsnws/event/1/query?format=geojson&starttime=2000-01-01&endtime=2019-12-31&minmagnitude=8&orderby=magnitude')
    .then(response => response.json())
    .then(earthquakeData => this.largeEarthquakes = earthquakeData.features)
    .then(banana => console.log(this.largeEarthquakes))
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 20px;
}

#app h1{
  text-align:center;
}
</style>
