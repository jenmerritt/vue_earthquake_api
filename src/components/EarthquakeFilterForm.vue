<template lang="html">
  <form v-on:submit.prevent id="find-filter-form">
    <input type="text" v-model="userDefinedStartTime" placeholder="Date Start format: yyyy-mm-dd">
    <input type="text" v-model="userDefinedEndTime" placeholder="Date End format: yyyy-mm-dd">
    <input type="text" v-model="userDefinedMagnitude" placeholder="Enter Minimum Magnitude">
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

#find-filter-form{
  margin: 0 auto;
  text-align:center;
  margin-bottom: 35px;
}

input[type=text]{
  padding:10px;
  margin:5px;
  width: 200px;
  font-size:14px;
}
input[type=submit]{
  padding: 10px 20px;
  background-color: lightgrey;
  cursor: pointer;
  color:black;
  font-size:14px;

}

input[type=submit]:hover{
  padding: 10px 20px;
  background-color: lightgrey;
  cursor: pointer;
  text-decoration:underline;
  font-size:14px;
}

</style>
