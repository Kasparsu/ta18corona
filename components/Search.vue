<template>
    <div class="columns">
      <div class="column is-three-quarters">
        <input class="input" type="text" placeholder="Country" v-model="search" @input="valueChanged">
      </div>
      <div class="column is-one-quarter">
        <div class="select">
          <select @input="valueChanged" v-model="sort">
            <option v-for="stat in allStats" :value="stat">{{stat}}</option>
          </select>
        </div>
      </div>
    </div>
</template>

<script>
    export default {
        name: "Search",
        data() {
          return {
            search: '',
            sort: null,
            stats: ['Confirmed', 'Deaths', 'Recovered']
          }
        },
      computed: {
        totalStats() {
          return this.stats.map(stat => 'Total' + stat);
        },
        newStats() {
          return this.stats.map(stat => 'New' + stat);
        },
        allStats() {
          let all = [];
          all.push(...this.newStats);
          all.push(...this.totalStats);
          return all;
        }
      },
      methods: {
        valueChanged(){
          this.$nextTick(() => {
            this.$emit('changed', {search: this.search, sort:this.sort});
          });
        }
      }
    }
</script>

<style scoped>

</style>
