<template lang="html">
  <div>
    <thead>
      <tr>
        <td>Location</td>
        <td>Magnitude</td>
        <td>MMI</td>
        <td>Date</td>
      </tr>
    </thead>
  <tr v-for="earthquake in earthquakes">
    <td>{{ earthquake.properties.place }}</td>
    <td>{{ earthquake.properties.mag }}</td>
    <td>{{ earthquake.properties.mmi }}</td>
    <!-- <td>{{ new Date(earthquake.properties.time) }}</td> -->
    <td>{{ createDate(earthquake) }}</td>
  </tr>
</div>
</template>

<script>
import {eventBus} from '../main.js';

export default {
  name: 'earthquakes-list',
  data(){
    return{
      earthquakes: []
    }
  },
  mounted(){
    eventBus.$on('earthquakes', (earthquakes) => {
      this.earthquakes = earthquakes
    });
  },
  methods: {
    createDate(earthquake) {
      const convertedDate = new Date(earthquake.properties.time);
      const dateString = convertedDate.toDateString();
      return dateString;
    }
  }
  // props: ['earthquakes']
}
</script>

<style lang="css" scoped>
td{
  padding: 20px;
  border-bottom: 1px solid #000;
}

tr{
  padding: 20px;
}

tr:nth-child(even) {
  background-color: #f2f2f2;
}

thead{
  font-weight: bold;
}
</style>
