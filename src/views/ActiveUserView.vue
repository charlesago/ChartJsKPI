<template>
  <div>
    <canvas id="activeUserChart" ref="activeUserChartRef"></canvas>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from 'vue';
import Chart from 'chart.js/auto';

export default defineComponent({
  name: 'ActiveUserView',
  setup() {
    const activeUserChartRef = ref<HTMLCanvasElement | null>(null);

    onMounted(async () => {
      const response = await fetch('http://localhost:8000/api/fake-data');
      const data = await response.json();

      if (activeUserChartRef.value) {
        new Chart(activeUserChartRef.value.getContext('2d') as CanvasRenderingContext2D, {
          type: 'bar',
          data: {
            labels: data.barChart.labels,
            datasets: [{
              label: 'Active Users',
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
    });

    return {
      activeUserChartRef
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
