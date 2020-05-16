<template>
  <div id="app" class="container">
    <!-- <LeafletMap /> -->
    <MarkerMap />
  </div>
</template>

<script>
// import LeafletMap from './components/LeafletMap.vue';
import MarkerMap from './components/MarkerMap.vue';
export default {
  name: 'App',
  data() {
    return {

    }
  },
  methods: {
  },
  components: {
    // LeafletMap, 
    MarkerMap,
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
</style>
