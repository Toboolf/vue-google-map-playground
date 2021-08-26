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
    container: {
      type: String,
      required: true
    }
  },

  methods: {
    buildKml(){
      const KmlLayer = this.google.maps.KmlLayer
      var kmlLayer = new KmlLayer(this.src, {
        suppressInfoWindows: true,
        preserveViewport: false,
        map: this.map
      })
      const container = this.container;
      kmlLayer.addListener('click', function(event) {
        var content = event.featureData.infoWindowHtml;
        var testimonial = document.getElementById(container);
        testimonial.innerHTML = content;
      });
    }
  },

  mounted(){
    this.buildKml()
  },
  render(){ return null }

}
</script>
