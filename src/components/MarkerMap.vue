<template>

  <div>
    <l-map
      :zoom="zoom"
      :center="center"
      style="height: 500px; width: 100%"
    >
      <l-tile-layer
        :url="url"
        :attribution="attribution"
      />
      <!-- Create HTML icon (divIcon) by providing content inside the l-icon tag -->
      <l-marker :key="index" v-for="(point, index) in points" :lat-lng="[point.latitude, point.longitude]">
        <l-icon
            :style="{ backgroundColor: point.color }"
            :icon-anchor="staticAnchor"
            :class-name="[point.shape == 'circle' ? 'circle' : 'square']"
        >
          <div>
          </div>
        </l-icon>
      </l-marker>
    </l-map>
  </div>
</template>

<script>
import { LMap, LTileLayer, LMarker, LIcon } from "vue2-leaflet";
import { latLng } from "leaflet";

export default {
  name: "MarkerMap",
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LIcon
  },
  data() {
    return {
        zoom: 13,
        center: latLng(47.41322, -1.219482),
        url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
        attribution:
        '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',

        points: [
            {
                latitude: 47.41322,
                longitude: -1.219482,
                shape: 'square',
                color: 'red',
            },
            {
                latitude: 47.41822,
                longitude: -1.239482,
                shape: 'circle',
                color: 'blue',
            }
        ],
        staticAnchor: [16, 37],
        customText: "Foobar",
        iconSize: 64
    };
  },
  computed: {
    dynamicSize() {
      return [this.iconSize, this.iconSize * 1.15];
    },
    dynamicAnchor() {
      return [this.iconSize / 2, this.iconSize * 1.15];
    }
  },
  methods: {}
};
</script>

<style>
.square {
  background-color: aqua;
  padding: 10px;
  border: 1px solid #333;

}

.circle {
    background-color: aqua;
    padding: 10px;
    border-radius: 50%;
    border: 1px solid #333;
}
</style>
