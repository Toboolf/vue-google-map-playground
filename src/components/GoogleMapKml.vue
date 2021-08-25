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
    src: {
      type: String,
      required: true
    },
    show: {
      type: Boolean,
      required: false,
      default: true
    },
  },

  methods: {
    buildKml() {
      const KmlLayer = this.google.map.KmlLayer
      var kmlLayer = new KmlLayer(this.src, {
        suppressInfoWindows: true,
        preserveViewport: false,
        map: this.map
      })
      kmlLayer.addListener('click', function(event) {
        console.log("Cliked my kml layer");
      });
    }
  }

}
</script>
