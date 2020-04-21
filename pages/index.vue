<template>
  <div class="section">
    <search @changed="setSearch"></search>
    <stats-list :countries="sortedCountries" :world="worldData" v-if="data"></stats-list>
  </div>
</template>

<script>

import Stats from "../components/Stats";
import StatsList from "../components/StatsList";
import Search from "../components/Search";
export default {
  components: {Search, StatsList, Stats},
  created() {
    this.$axios.$get('https://api.covid19api.com/summary').then(resp => {
      this.data = resp;
    });
  },
  data(){
    return {
      data: null,
      search: '',
      sort: null
    }
  },
  methods: {
    setSearch({search, sort}){
      this.search = search;
      this.sort = sort;
    }
  },
  computed: {
    worldData(){
      return {Country: 'World', ...this.data.Global}
    },
    filteredCountries(){
      return this.data.Countries.filter(country => {
        let len = this.search.length;
        return country.Country.substr(0, len).toLowerCase().trim() === this.search.toLowerCase().trim();
      });
    },
    sortedCountries(){
      let countries = JSON.parse(JSON.stringify(this.filteredCountries));
      return countries.sort((a,b) => {
        if(a[this.sort] < b [this.sort]) {
          return 1;
        }
        if(a[this.sort] > b [this.sort]){
          return -1;
        }
        return 0;
      });
    }
  }
}
</script>

<style>

</style>
