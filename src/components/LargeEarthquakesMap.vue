<template lang="html">
  <div id="map-wrap">
    <h2>Distribution of all historical earthquakes over 8.0 magnitude</h2>
          <div id="mapid" ref="mapElement">
          </div>
  </div>
</template>

<script>

export default {
  name: 'large-earthquake-map',
  props: ['largeEarthquakes', 'largeEarthquakesCoordinates'],
  data(){
    return{
    }
  },
  methods:{

    },
  mounted() {

      var mymap = L.map(this.$refs['mapElement']).setView([51.505, -0.09], 1);
    
      L.tileLayer('https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token=pk.eyJ1IjoiamVuam9tZXoiLCJhIjoiY2s1bGU5M3M2MGx4dzNybGJvbW5obHV6YyJ9.o2Q4Hjeyc5dldKlvGW95vQ', {
              attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
              maxZoom: 18,
              id: 'mapbox/streets-v11',
              accessToken: 'your.mapbox.access.token'
            }).addTo(mymap);

        // marker is [lat , long]
      this.largeEarthquakesCoordinates.forEach( set => L.marker([set[1], set[0]]).addTo(mymap) );


  }
}
</script>

<style lang="css" scoped>

#map-wrap{
  text-align:center;
}

#mapid{
  height:300px;
  max-width: 40%;
  margin: 0 auto;
}

</style>
