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
    }
  },

  data() { return {
    self: null
  }},

  watch: {
    show() {
      if (this.show) {
        this.self.setMap(null)
      } else {
        this.self.setMap(this.map)
      }
    }
  },

  mounted() {
    const { Marker } = this.google.maps;

    this.self = new Marker({
      position: this.marker.position,
      marker: this.marker,
      map: this.map,
      //icon: POINT_MARKER_ICON_CONFIG
    });
  },

  render() { return null }
};
</script>
