<template>
  <canvas ref="myChart"></canvas>
</template>

<script>
    import Chart from "chart.js";

    export default {
        name: "Chart",
        props: ['labels', 'data'],
        data() {
          return {

          }
        },
        mounted() {
          var myChart = new Chart(this.$refs['myChart'],{
            type: 'line',
            data: {
              labels: this.labels,
              datasets: [{
                label: '# of Votes',
                data: this.data,
                borderWidth: 1
              }]
            },
            options: {
              scales: {
                yAxes: [{
                  ticks: {
                    beginAtZero: true
                  }
                }]
              }
            }
          });
        }
    }
</script>

<style scoped>

</style>
