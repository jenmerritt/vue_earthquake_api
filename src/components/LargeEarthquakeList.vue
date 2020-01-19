<template lang="html">
  <div>
    <h3>Earthquakes from 2000 - 2020 with magnitude over 8.0</h3>
    <!-- <ul>
      <li v-for="earthquake in largeEarthquakes">
        <dl>
          <dt>Location:</dt>
          <dd>{{ earthquake.properties.place }}</dd>
          <dt>Magnitude:</dt>
          <dd>{{ earthquake.properties.mag }}</dd>
          <dt>MMI:</dt>
          <dd>{{ earthquake.properties.mmi }}</dd>
          <dt>Date:</dt>
          <dd>{{ new Date(earthquake.properties.time) }}</dd>
        </dl>
        <hr/>
      </li>
    </ul> -->
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
      <!-- <td>{{ new Date(earthquake.properties.time) }}</td> -->
      <td>{{ createDate(earthquake) }}</td>
    </tr>

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
