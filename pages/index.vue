<template>
  <div class="section">
    <search></search>
    <stats-list :countries="$store.getters.sortedCountries" :world="$store.getters.globalAsCountry" v-if="$store.state.countries"></stats-list>
  </div>
</template>

<script>

import StatsList from "../components/StatsList";
import Search from "../components/Search";
export default {
  components: {Search, StatsList},
  created() {
    this.$store.dispatch('fetchStatistics');
  }
}
</script>

<style>

</style>
