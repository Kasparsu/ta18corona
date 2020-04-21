<template>
  <div class="card">
    <header class="card-header has-background-info">
      <p class="card-header-title">
        {{data.Country}}
      </p>
      <img v-if="data.CountryCode" :src="flagUrl">
    </header>
    <div class="card-content">
      <table>
        <tbody>
          <tr v-for="stat in allStats" :key="stat">
            <td>{{stat}}</td>
            <td class="has-text-right">{{data[stat]}}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
    export default {
        name: "Stats",
        props: ['data'],
        data() {
          return {
            stats: ['Confirmed', 'Deaths', 'Recovered']
          }
        },
        computed: {
          flagUrl(){
            return `https://www.countryflags.io/${this.data.CountryCode.toLowerCase()}/flat/64.png`;
          },
          totalStats(){
            return this.stats.map(stat => 'Total' + stat);
          },
          newStats(){
            return this.stats.map(stat => 'New' + stat);
          },
          allStats(){
            let all = [];
            all.push(...this.newStats);
            all.push(...this.totalStats);
            return all;
          }
        }
    }
</script>

<style scoped>
  table {
    width: 100%;
  }
</style>
