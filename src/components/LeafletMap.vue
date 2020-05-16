<template>
    <div class="container">
        <div class="row">
            <div class="col-12">

                <h1 class="text-center text-info">LeafletMap</h1>

            </div>
        </div>

        <div class="row">
            <div class="col-6">
                <PointList :points="points" />
            </div>
            <div class="col-6">
                <Map/>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios';
import PointList from './PointList.vue';
import Map from './Map.vue';

export default {
    name: 'LeafletMap',
    data: function() {
        return {
            points: [],
        }
    },
    components: {
        PointList, Map,
    },
    mounted: function() {
        console.log("mounted")
        axios.get('https://api.openbrewerydb.org/breweries')
            .then((response) => {
                this.points = response.data;
            })
    },
    methods: {

    }
}
</script>

<style lang="scss" scoped>

</style>