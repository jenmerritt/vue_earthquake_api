<template>
  <div id="app">
    <h1>Earthquake Tracker</h1>
    <earthquake-filter-form />
    <earthquakes-list />
    <large-earthquake-list v-bind:largeEarthquakes="largeEarthquakes" />

    <!-- v-bind:userDefinedStartTime="userDefinedStartTime" v-bind:userDefinedEndTime="userDefinedEndTime" v-bind:userDefinedMagnitude="userDefinedMagnitude" -->
  </div>
</template>

<script>
import {eventBus} from './main.js';
import LargeEarthquakeList from './components/LargeEarthquakeList.vue';
import EarthquakeFilterForm from './components/EarthquakeFilterForm.vue';
import EarthquakesList from './components/EarthquakesList.vue';

export default {
  name: 'app',
  components: {
    "large-earthquake-list": LargeEarthquakeList,
    "earthquake-filter-form": EarthquakeFilterForm,
    "earthquakes-list": EarthquakesList
  },
  data(){
    return {
      largeEarthquakes: [],
      // earthquakes: [],
      // userDefinedStartTime: "",
      // userDefinedEndTime: "",
      // userDefinedMagnitude: ""
    };
  },
  mounted() {

    fetch('https://earthquake.usgs.gov/fdsnws/event/1/query?format=geojson&starttime=2000-01-01&endtime=2019-12-31&minmagnitude=8&orderby=magnitude')
    .then(response => response.json())
    .then(earthquakeData => this.largeEarthquakes = earthquakeData.features);
    // .then(viewData => console.log(this.largeEarthquakes));

      // eventBus.$on('start-time', (date) => {
      //   this.userDefinedStartTime = date
      // });
      //
      // eventBus.$on('end-time', (date) => {
      //   this.userDefinedEndTime = date
      // });
      //
      // eventBus.$on('magnitude', (magnitude) => {
      //   this.userDefinedMagnitude = magnitude
      // });

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
