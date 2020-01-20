<template lang="html">
  <div>
    <table>
      <thead>
        <tr>
          <td></td>
          <td>Location</td>
          <td>Magnitude</td>
          <td>MMI</td>
          <td>Date</td>
        </tr>
      </thead>
      <tbody>
        <tr v-if="this.earthquakes.length === 0">
          <td>No data to display. Please try different criteria.</td>
        </tr>
        <tr v-for="(earthquake, index) in earthquakes">
          <td>{{ (index+1) }}</td>
          <td>{{ earthquake.properties.place }}</td>
          <td>{{ earthquake.properties.mag }}</td>
          <td>{{ earthquake.properties.mmi }}</td>
          <td>{{ createDate(earthquake) }}</td>
          <td>{{  }}</td>
        </tr>
      </tbody>
    </table>
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
