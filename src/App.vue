<template>
  <div id="app">
    <div id="headerbar">
      <h1>Earthquakes App</h1>
      <ul id="menu">
        <li class="menu-item" v-on:click="loadHome">Home</li>
        <li class="menu-item" v-on:click="loadLargeEarthquakes">Large Earthquakes</li>
        <li class="menu-item" v-on:click="loadEarthquakeFinder">Earthquake Finder</li>
      </ul>
    </div>
    <div id="landing-page" v-if="landingpageseen">
      <landing-page />
    </div>
    <div id="custom-earthquake" v-if="earthquakeselectorseen">
      <earthquake-filter-form />
      <earthquakes-list />
    </div>
    <div id="large-earthquakes">
      <large-earthquakes-map v-bind:largeEarthquakes="largeEarthquakes" v-bind:largeEarthquakesCoordinates="largeEarthquakesCoordinates" v-if="largeearthquakesseen" />
      <large-earthquake-list v-bind:largeEarthquakes="largeEarthquakes" v-if="largeearthquakesseen" />
    </div>
  </div>
</template>

<script>
import {eventBus} from './main.js';
import LargeEarthquakeList from './components/LargeEarthquakeList.vue';
import EarthquakeFilterForm from './components/EarthquakeFilterForm.vue';
import EarthquakesList from './components/EarthquakesList.vue';
import LargeEarthquakesMap from './components/LargeEarthquakesMap.vue';
import LandingPage from './components/LandingPage.vue';


export default {
  name: 'app',
  components: {
    "large-earthquake-list": LargeEarthquakeList,
    "earthquake-filter-form": EarthquakeFilterForm,
    "earthquakes-list": EarthquakesList,
    "large-earthquakes-map": LargeEarthquakesMap,
    "landing-page": LandingPage
  },
  data(){
    return {
      largeEarthquakes: [],
      largeEarthquakesCoordinates: [],
      landingpageseen: true,
      earthquakeselectorseen: false,
      largeearthquakesseen: false
    };
  },
  mounted() {

    fetch('https://earthquake.usgs.gov/fdsnws/event/1/query?format=geojson&starttime=1700-01-01&endtime=2021-01-01&minmagnitude=8&orderby=magnitude')
    .then(response => response.json())
    .then(earthquakeData => this.largeEarthquakes = earthquakeData.features)
    .then(() => this.largeEarthquakesCoordinates = this.createArrayOfEarthquakeLocations())
  },
  methods:{

      createArrayOfEarthquakeLocations(){
        let locations = []
        this.largeEarthquakes.forEach( quake => locations.push([quake.geometry.coordinates[0], quake.geometry.coordinates[1]]))
        return locations
      },

    loadHome(){
      this.landingpageseen = true;
      this.earthquakeselectorseen = false;
      this.largeearthquakesseen = false;
    },

    loadLargeEarthquakes(){
      this.landingpageseen = false;
      this.earthquakeselectorseen = false;
      this.largeearthquakesseen = true;
    },

    loadEarthquakeFinder(){
      this.landingpageseen = false;
      this.earthquakeselectorseen = true;
      this.largeearthquakesseen = false;
    }

  }
}

</script>

<style>

html, body {
  margin: 0;
  padding:0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

#app h1{
  text-align:center;
  margin: 0;
}

#headerbar{
  padding: 20px 0 20px 0;
  margin-bottom: 50px;
  background-color: midnightblue;
}

#headerbar h1 {
  color: white;
  margin-bottom: 10px;
  font-size: 38px;
}

#map { height: 300px; }

.visible{
  visibility: visible;
}

.hidden{
  visibility: hidden;
}

#menu {
  width: 500px;
  display: flex;
  justify-content: center;
  margin: 0 auto;
  color: white;
  font-size: 18px;
}

.menu-item {
  display: inline-block;
  flex-grow: 1;
}

.menu-item:hover{
  text-decoration: underline;
  cursor: pointer;

}

.menu-item:visited{
  text-decoration: none;
}

</style>
