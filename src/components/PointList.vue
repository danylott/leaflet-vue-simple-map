<template>
    <div class="card leaflet-map" style="width: 18rem;">
        <ul class="list-group list-group-flush">
            <li :key="index"
                v-for="(point, index) in points"
                class="list-group-item"
                >{{ point.name }}, {{ point.state }}</li>
        </ul>
    </div>
</template>

<script>
export default {
    name: 'PointList',
    props: {
        points: Array,
    }
}
</script>

<style lang="scss" scoped>
    .leaflet-map {
        overflow: scroll;
        height: 95vh;
        li {
            &:hover {
                background-color: darkgray;
            }
        }
    }
</style>
