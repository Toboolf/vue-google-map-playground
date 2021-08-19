<template>
  <div id="app">
    <h1>Google Maps implementation with Vue JS</h1>
    
    <div>
      <GoogleMapLoader class="map-container"
        apiKey=""
        :mapConfig="mapConfig"
      >
        <template slot-scope="{ google, map }">
          <GoogleMapMarker
            v-for="marker in markers"
            :key="marker.id"
            :marker="marker"
            :google="google"
            :map="map"
            :show="showMarkers"
          />
          <div>
            <button @click="centerMap(map)">Center</button>
            <button @click="showMarkers = !showMarkers">Show Markers</button>
          </div>
        </template>
      </GoogleMapLoader>
    </div>
  </div>
</template>

<script>
import GoogleMapLoader from './components/GoogleMapLoader.vue'
import GoogleMapMarker from './components/GoogleMapMarker.vue'

export default {
  name: 'App',
  components: {
    GoogleMapLoader,
    GoogleMapMarker
  },
  data() {
    return {
      mapConfig: {
        center: { lat: 19.48698, lng: -99.18594 },
        zoom: 13
      },
      markers: [
        { id: "a", position: { lat: 19.48698, lng: -99.18594 } },
        { id: "b", position: { lat: 19.50, lng: -99.186 } },
        { id: "c", position: { lat: 19.51, lng: -99.1861 } }
      ],
      showMarkers: true
    }
  },
  methods: {
    centerMap(map) { map.setCenter(this.mapConfig.center) }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.map-container {
  height: 700px;
}
</style>
