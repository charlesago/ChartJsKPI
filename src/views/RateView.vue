<template>
  <div>
    <canvas id="rateChart" ref="rateChartRef"></canvas>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from 'vue';
import Chart from 'chart.js/auto';

export default defineComponent({
  name: 'RateView',
  setup() {
    const rateChartRef = ref<HTMLCanvasElement | null>(null);

    onMounted(async () => {
      const response = await fetch('http://localhost:8000/api/fake-data');
      const data = await response.json();

      if (rateChartRef.value) {
        new Chart(rateChartRef.value.getContext('2d') as CanvasRenderingContext2D, {
          type: 'line',
          data: {
            labels: data.lineChart.labels,
            datasets: [{
              label: 'Rate',
              data: data.lineChart.data,
              backgroundColor: 'rgba(255, 159, 64, 0.2)',
              borderColor: 'rgba(255, 159, 64, 1)',
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
      rateChartRef
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
