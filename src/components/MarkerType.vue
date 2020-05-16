<template>
    <div>
        <h1>Select Marker Type</h1>
        <div :key="index" @click="changeMarkerType(marker)" :class="[currentShape == marker ? 'selected' : '', marker] " v-for="(marker, index) in markers"></div>
    </div>

</template>
<script>
export default {
    name: 'MarkerType',
    data() {
        return {
            markers: ['circle', 'square'],
        }
    },
    props: ['currentShape'],
    methods: {
        changeMarkerType(marker) {
            console.log(marker);
            console.log(this.currentShape);
            this.$emit('set-shape', marker);
        }
    }
}
</script>

<style lang="scss" scoped>
.selected {
    height: 20px;
    background-color: darkgray;
}
</style>