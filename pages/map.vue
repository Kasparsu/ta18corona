<template>
    <leaflet-map :center="[-49,-42]" :zoom="4" :geoJSON="this.$store.getters.confirmedGeoJSON"></leaflet-map>
</template>

<script>
    import LeafletMap from "../components/LeafletMap";
    export default {
      components: {LeafletMap},
      created() {
        this.$store.dispatch('fetchStatistics');
        this.$store.dispatch('fetchGeoJSON');
      }
    }
</script>

<style scoped>

</style>
