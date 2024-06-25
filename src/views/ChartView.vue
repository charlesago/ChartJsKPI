<template>
  <div>
    <canvas id="barChart" ref="barChartRef"></canvas>
    <canvas id="lineChart" ref="lineChartRef"></canvas>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from 'vue';
import Chart from 'chart.js/auto';

export default defineComponent({
  name: 'ChartView',
  setup() {
    const barChartRef = ref<HTMLCanvasElement | null>(null);
    const lineChartRef = ref<HTMLCanvasElement | null>(null);

    onMounted(async () => {
      const response = await fetch('http://localhost:8000/api/fake-data');
      const data = await response.json();

      if (barChartRef.value) {
        new Chart(barChartRef.value.getContext('2d') as CanvasRenderingContext2D, {
          type: 'bar',
          data: {
            labels: data.barChart.labels,
            datasets: [{
              label: '# of Votes',
              data: data.barChart.data,
              backgroundColor: 'rgba(75, 192, 192, 0.2)',
              borderColor: 'rgba(75, 192, 192, 1)',
              borderWidth: 1
            }]
          },
          options: {
            scales: {
              y: {
                beginAtZero: true
              }
            }
          }
        });
      }

      if (lineChartRef.value) {
        new Chart(lineChartRef.value.getContext('2d') as CanvasRenderingContext2D, {
          type: 'line',
          data: {
            labels: data.lineChart.labels,
            datasets: [{
              label: '# of Votes',
              data: data.lineChart.data,
              backgroundColor: 'rgba(153, 102, 255, 0.2)',
              borderColor: 'rgba(153, 102, 255, 1)',
              borderWidth: 1
            }]
          },
          options: {
            scales: {
              y: {
                beginAtZero: true
              }
            }
          }
        });
      }
    });

    return {
      barChartRef,
      lineChartRef
    };
  }
});
</script>

<style scoped>
canvas {
  max-width: 600px;
  margin: 20px;
}
</style>
