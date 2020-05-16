<template>

  <div>
    <h1>Cool Map</h1>
    <l-map
      @click="addMarker"
      :zoom="zoom"
      :center="center"
      style="height: 500px; width: 100%"
    >
      <l-tile-layer
        :url="url"
        :attribution="attribution"
      />

      <l-marker :key="index" v-for="(point, index) in points" @click="removeMarker(index)" :lat-lng="[point.latitude, point.longitude]">
        <l-icon
            :style="{ backgroundColor: point.color }"
            :icon-anchor="staticAnchor"
            :class-name="point.shape"
        >
          <div>
          </div>
        </l-icon>
      </l-marker>
    </l-map>
    <div class="row">
      <div class="col-6">
        <MarkerType @set-shape="setShape" :currentShape="currentShape" />
      </div>
      <div class="col-6">
        
      </div>
    </div>
  </div>
</template>

<script>
import { LMap, LTileLayer, LMarker, LIcon } from "vue2-leaflet";
import { latLng } from "leaflet";

import MarkerType from './MarkerType';

export default {
  name: "MarkerMap",
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LIcon,
    MarkerType,
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
        staticAnchor: [16, 16],
        currentShape: 'circle',
        currentColor: 'green',
    };
  },
  methods: {
    removeMarker(index) {
      this.points.splice(index, 1);
    },
    addMarker(event) {
      console.log(event.latlng);
      this.points.push({
          latitude: event.latlng.lat,
          longitude: event.latlng.lng,
          shape: this.currentShape,
          color: this.currentColor,
      });
    },
    setShape(marker) {
      this.currentShape = marker;
    }
  }
};
</script>

<style>
.square {
  background-color: aqua;
  padding: 10px;
  margin: 10px;
  display: inline;
  border: 1px solid #333;

}

.circle {
  display: inline;
  background-color: aqua;
  padding: 10px;
  margin: 10px;
  border-radius: 50%;
  border: 1px solid #333;
}
</style>
