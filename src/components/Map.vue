<template>

  <div style="height: 95vh; width: 100%">
    <div style="height: 200px overflow: auto;">
      <p>Center is at {{ currentCenter }} and the zoom is: {{ currentZoom }}</p>
      <button @click="showLongText">
        Toggle long popup
      </button>
      <button @click="showMap = !showMap">
        Toggle map
      </button>
    </div>
    <l-map
      v-if="showMap"
      :zoom="zoom"
      :center="center"
      :options="mapOptions"
      style="height: 80%"
      @update:center="centerUpdate"
      @update:zoom="zoomUpdate"
    >
      <l-tile-layer
        :url="url"
        :attribution="attribution"
      />
      <l-marker 
        :key="index" 
        v-for="(point, index) in points" 
        :lat-lng="latLngMethod(point.latitude, point.longitude)"
        >
        <l-icon class="leaflet-div-icon" >

        </l-icon>
        <l-popup>
          <div @click="innerClick">
            {{ point.name }}
            <p v-show="showParagraph">
              city: {{ point.city }}, country: {{ point.country }}, website_url {{ point.website_url }}
            </p>
          </div>
        </l-popup>
      </l-marker>
    </l-map>
  </div>
</template>

<script>
import { latLng } from "leaflet";
import { LMap, LIcon, LTileLayer, LMarker, LPopup } from "vue2-leaflet";

export default {
  name: "Example",
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LPopup,
    LIcon,
  },
  data() {
    return {
      zoom: 13,
      center: latLng(47.41322, -1.219482),
      url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      attribution:
        '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      currentZoom: 11.5,
      currentCenter: latLng(33.524521, -86.774322),
      showParagraph: false,
      mapOptions: {
        zoomSnap: 0.5
      },
      showMap: true
    };
  },
  props: {
      points: Array,
  },
  methods: {
    latLngMethod(latitude, longitude) {
        return latLng(latitude, longitude);
    },
    zoomUpdate(zoom) {
      this.currentZoom = zoom;
    },
    centerUpdate(center) {
      this.currentCenter = center;
    },
    showLongText() {
      this.showParagraph = !this.showParagraph;
    },
    innerClick() {
      alert("Click!");
    }
  }
};
</script>

<style lang="scss" scoped>
.leaflet-div-icon {
    background: #fff;
    border: 1px solid #666;
}
</style>