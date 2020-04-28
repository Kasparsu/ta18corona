<template>
  <div>
    <canvas ref="myChart"></canvas>
    <slot></slot>
  </div>
</template>

<script>
    import Chart from "chart.js";

    export default {
        name: "Chart",
        props: ['labels', 'data'],
        data() {
          return {
            chart: null
          }
        },
        updated() {
          this.chart.data.datasets = this.$children.map(dataset => {
            return  {
              label: dataset.title,
              data: dataset.data,
              borderColor: dataset.color,
              backgroundColor: dataset.color
            }
          });
          this.chart.update();
        },
      watch: {
          labels(labels, oldLabels){
            this.chart.data.labels = labels;
            this.chart.update();
          },
          data(data, oldData){
            this.chart.data.datasets[0].data = data;
            this.chart.update();
          }
        },
        mounted() {
          this.chart = new Chart(this.$refs['myChart'],{
            type: 'line',
            data: {
              labels: this.labels
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
