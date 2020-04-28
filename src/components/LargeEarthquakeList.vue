<template lang="html">
  <div id="large-earthquakes-wrap">
    <h3>Earthquakes with magnitude over 8.0</h3>
    <table id="large-earthquakes-table">
      <thead>
        <tr>
          <td>Location</td>
          <td>Magnitude</td>
          <td>MMI</td>
          <td>Date</td>
        </tr>
      </thead>
      <tr v-for="earthquake in largeEarthquakes">
        <td>{{ earthquake.properties.place }}</td>
        <td>{{ earthquake.properties.mag }}</td>
        <td>{{ earthquake.properties.mmi }}</td>
        <td>{{ createDate(earthquake) }}</td>
        <td><a :href="earthquake.properties.url" target="_blank">More info</a></td>
      </tr>
    </table>

  </div>
</template>

<script>

export default {
  name: 'large-earthquake-list',
  props: ['largeEarthquakes'],
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

#large-earthquakes-wrap {
  text-align: center;
}

#large-earthquakes-table {
  margin: 0 auto;
}

dd{
  text-align:left;
  margin: 0;
  padding:0;
}
dt{
  text-align:left;
  font-weight:bold;
}

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
