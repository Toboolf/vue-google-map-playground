<template>
  <div id="app">
    <h1>Google Maps implementation with Vue JS</h1>
    <div id="kmlcontent"></div>
    <div>
      <GoogleMapLoader class="map-container"
        apiKey="AIzaSyCI1A_1VmLyt7lM5eUdLNCXJSuC36hnYSs"
        :mapConfig="mapConfig"
      >
        <template slot-scope="{ google, map }">\
          <GoogleMapKml
            :google="google"
            :map="map"
            container="kmlcontent"
            src="https://www.google.com/maps/d/u/1/kml?forcekml=1&mid=197LDSkNzpeIdBjgGBoGbMCylzitqnZyf"/>
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
            <button @click="changeTrees">Change trees</button>
          </div>
        </template>
      </GoogleMapLoader>
    </div>
  </div>
</template>

<script>
import GoogleMapLoader from './components/GoogleMapLoader.vue'
import GoogleMapMarker from './components/GoogleMapMarker.vue'
import GoogleMapKml from './components/GoogleMapKml.vue'

export default {
  name: 'App',
  components: {
    GoogleMapLoader,
    GoogleMapMarker,
    GoogleMapKml
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
    centerMap(map) { map.setCenter(this.mapConfig.center) },
    async changeTrees() {
      this.show.trees = false
      await this.sleep(2000)
      console.log("timed out");
      this.trees = [
        { id: "x", position: { lat: 19.47, lng: -99.18594 } },
        { id: "y", position: { lat: 19.46, lng: -99.186 } },
        { id: "z", position: { lat: 19.45, lng: -99.1861 } }
      ]
      this.show.trees = true
    },
    sleep(ms) {
      return new Promise(resolve => setTimeout(resolve, ms));
    }
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
