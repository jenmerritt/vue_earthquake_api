<template lang="html">
  <section id="landing-page-wrap">
    <p>This web app uses data from the extensive <a href="https://earthquake.usgs.gov/fdsnws/event/1/">USGS Earthquakes API</a>.</p>
    <h2>Features:</h2>
    <ul id="features-list">
      <li>View a map of the largest Earthquakes in history</li>
      <li>Enter your own criteria to find a period of time or magnitude that interests you</li>
    </ul>
  </section>
</template>

<script>
export default {
}
</script>

<style lang="css" scoped>

#landing-page-wrap{
  text-align: center;
}

#features-list{
  list-style-position: inside;
  padding: 0;
}


</style>
