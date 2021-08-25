<script>
export default {
  props: {
    google: {
      type: Object,
      required: true
    },
    map: {
      type: Object,
      required: true
    },
    marker: {
      type: Object,
      required: true
    },
    show: {
      type: Boolean,
      required: false,
      default: true
    },
    icon: {
      type: String,
      required: false
    }
  },

  data() { return {
    self: null
  }},

  watch: {
    show: function() {
      if (!this.show) {
        this.self.setMap(null)
      } else {
        this.self.setMap(this.map)
      }
    }
  },

  methods: {
    buildMarker() {
      const { Marker } = this.google.maps;

      const makerDefinition = {
        position: this.marker.position,
        marker: this.marker,
        map: this.map
      }

      if(this.icon) {
        const markerIcon = {
          url: require(`../assets/${this.icon}`),
          size: new this.google.maps.Size(25, 25),
          origin: new this.google.maps.Point(0, 0),
          anchor: new this.google.maps.Point(10, 25),
          scaledSize: new this.google.maps.Size(25, 25)
        }
        makerDefinition.icon = markerIcon
      }

      this.self = new Marker(makerDefinition);

      this.self.addListener("click", () => {
        console.log("me pinchaste");
      });
    }
  },

  mounted() {
    this.buildMarker()
  },

  render() { return null }
};
</script>
