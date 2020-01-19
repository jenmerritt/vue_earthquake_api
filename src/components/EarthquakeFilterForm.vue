<template lang="html">
  <form v-on:submit.prevent>
    <input type="text" v-model="userDefinedStartTime" placeholder="Start format: yyyy-mm-dd">
    <input type="text" v-model="userDefinedEndTime" placeholder="End format: yyyy-mm-dd">
    <input type="text" v-model="userDefinedMagnitude" placeholder="Enter Magnitude">
    <!-- <button v-on:click="handleClick">Enter</button> -->
    <input type="submit" v-on:click="handleClick">
  </form>
</template>

<script>
import {eventBus} from '../main.js';

export default {
  name: 'earthquake-filter-form',
  data(){
    return{
      userDefinedStartTime: "",
      userDefinedEndTime: "",
      userDefinedMagnitude: "",
      earthquakes: []
   }
  },
  methods: {

    handleClick() {

      fetch(`https://earthquake.usgs.gov/fdsnws/event/1/query?format=geojson&starttime=${this.userDefinedStartTime}&endtime=${this.userDefinedEndTime}&minmagnitude=${this.userDefinedMagnitude}`)
        .then(response => response.json())
        .then(earthquakeData => this.earthquakes = earthquakeData.features);

        eventBus.$emit('earthquakes', this.earthquakes)


    }
  }

  }
</script>

<style lang="css" scoped>
</style>
