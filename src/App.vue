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
            v-for="marker in trees"
            :key="marker.id"
            :marker="marker"
            :google="google"
            :map="map"
            :show="show.trees"
            icon="tree.png"
          />
          <GoogleMapMarker
            v-for="marker in drops"
            :key="marker.id"
            :marker="marker"
            :google="google"
            :map="map"
            :show="show.drops"
            icon="drop.png"
          />
          <div>
            <button @click="centerMap(map)">Center</button>
            <button @click="show.trees = !show.trees">{{show.trees ? 'Show':'Hide'}} Trees</button>
            <button @click="show.drops = !show.drops">{{show.drops ? 'Show':'Hide'}} drops</button>
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
      trees: [
        { id: "a", position: { lat: 19.48698, lng: -99.18594 } },
        { id: "b", position: { lat: 19.50, lng: -99.186 } },
        { id: "c", position: { lat: 19.51, lng: -99.1861 } }
      ],
      drops: [
        { id: "d", position: { lat: 19.49, lng: -99.20 } },
        { id: "e", position: { lat: 19.50, lng: -99.21 } },
        { id: "f", position: { lat: 19.51, lng: -99.22 } }
      ],
      show: {
        trees: true,
        drops: true
      }
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
