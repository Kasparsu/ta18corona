<template>
  <div class="section">
      <button class="button is-danger" @click="toggleActive('deaths')">deaths</button>
      <button class="button is-warning" @click="toggleActive('confirmed')">confirmed</button>
      <button class="button is-success" @click="toggleActive('recovered')">recovered</button>
      <chart :labels="$store.getters.timelineLabels">
        <dataset v-if="active.includes('confirmed')" :data="$store.getters.timelineData['confirmed']" title="# of Confirmed Cases" color="rgba(255, 204, 0, 0.5)"></dataset>
        <dataset v-if="active.includes('deaths')" :data="$store.getters.timelineData['deaths']" title="# of Death Cases" color="rgba(255, 80, 80, 0.5)"></dataset>
        <dataset v-if="active.includes('recovered')" :data="$store.getters.timelineData['recovered']" title="# of Recovered Cases" color="rgba(63,255,37,0.5)"></dataset>
      </chart>
  </div>
</template>

<script>

    import Chart from "../components/Chart";
    import Dataset from "../components/Dataset";
    export default {
      components: {Dataset, Chart},
      created() {
          this.$store.dispatch('fetchTimeline', {slug:this.$route.params.slug, type: 'confirmed'});
        this.$store.dispatch('fetchTimeline', {slug:this.$route.params.slug, type: 'deaths'});
        this.$store.dispatch('fetchTimeline', {slug:this.$route.params.slug, type: 'recovered'})
      },
      data() {
        return {
          active: [
            'confirmed'
          ]
        }
      },
      methods: {
        toggleActive(type){
          if(this.active.includes(type)){
            this.active = this.active.filter(el => el!==type);
          } else {
            this.active.push(type);
          }

        }
      }

    }
</script>

<style scoped>

</style>
