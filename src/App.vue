<template>
  <div id="app">
    <h1>Earthquake Tracker App</h1>
    <earthquake-filter-form />
    <display-map />
    <earthquakes-list />
    <!-- <large-earthquake-list v-bind:largeEarthquakes="largeEarthquakes" /> -->
  </div>
</template>

<script>
import {eventBus} from './main.js';
import LargeEarthquakeList from './components/LargeEarthquakeList.vue';
import EarthquakeFilterForm from './components/EarthquakeFilterForm.vue';
import EarthquakesList from './components/EarthquakesList.vue';
import DisplayMap from './components/DisplayMap.vue';

export default {
  name: 'app',
  components: {
    "large-earthquake-list": LargeEarthquakeList,
    "earthquake-filter-form": EarthquakeFilterForm,
    "earthquakes-list": EarthquakesList,
    "display-map": DisplayMap
  },
  data(){
    return {
      largeEarthquakes: []
    };
  },
  mounted() {

    // fetch('https://earthquake.usgs.gov/fdsnws/event/1/query?format=geojson&starttime=2000-01-01&endtime=2019-12-31&minmagnitude=8&orderby=magnitude')
    // .then(response => response.json())
    // .then(earthquakeData => this.largeEarthquakes = earthquakeData.features);

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

#map { height: 300px; }

</style>
