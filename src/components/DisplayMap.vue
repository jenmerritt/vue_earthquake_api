<template lang="html">
  <div>
    <p>Map</p>
    <div id="mapid" ref="mapElement">

    </div>
  </div>
</template>

<script>

// import L from 'leaflet';

export default {


  mounted() {
    var mymap = L.map(this.$refs['mapElement']).setView([51.505, -0.09], 13);

    L.tileLayer('https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token=pk.eyJ1IjoiamVuam9tZXoiLCJhIjoiY2s1bGU5M3M2MGx4dzNybGJvbW5obHV6YyJ9.o2Q4Hjeyc5dldKlvGW95vQ', {
      attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
      maxZoom: 18,
      id: 'mapbox/streets-v11',
      accessToken: 'your.mapbox.access.token'
    }).addTo(mymap);

    var marker = L.marker([51.5, -0.09]).addTo(mymap);
      },
}
</script>

<style lang="css" scoped>

#mapid{
  height:300px;
}

</style>
