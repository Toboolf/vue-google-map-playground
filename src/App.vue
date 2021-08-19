<template>
  <div id="app">
    <h1>Google Maps implementation with Vue JS</h1>
    
    <div>
      <GoogleMapLoader class="map-container"
        apiKey=""
        :mapConfig="mapConfig"
      >
        <template slot-scope="{ map }">
          <div>
            <button @click="centerMap(map)">Center</button>
          </div>
        </template>
      </GoogleMapLoader>
    </div>
  </div>
</template>

<script>
import GoogleMapLoader from './components/GoogleMapLoader.vue'

export default {
  name: 'App',
  components: {
    GoogleMapLoader
  },
  data() {
    return {
      center: { lat: 19.48698, lng: -99.18594 },
      mapConfig: {
        center: { lat: 19.48698, lng: -99.18594 },
        zoom: 13
      }
    }
  },
  methods: {
    centerMap(map) { map.setCenter(this.center) }
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
