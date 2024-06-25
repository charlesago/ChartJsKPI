<template>
  <div>
    <canvas id="pieChart" ref="pieChartRef"></canvas>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from 'vue';
import Chart from 'chart.js/auto';

export default defineComponent({
  name: 'PieView',
  setup() {
    const pieChartRef = ref<HTMLCanvasElement | null>(null);

    onMounted(async () => {
      const response = await fetch('http://localhost:8000/api/fake-data');
      const data = await response.json();

      if (pieChartRef.value) {
        new Chart(pieChartRef.value.getContext('2d') as CanvasRenderingContext2D, {
          type: 'pie',
          data: {
            labels: data.pieChart.labels,
            datasets: [{
              label: '# of Votes',
              data: data.pieChart.data,
              backgroundColor: [
                'rgba(255, 99, 132, 0.2)',
                'rgba(54, 162, 235, 0.2)',
                'rgba(255, 206, 86, 0.2)',
                'rgba(75, 192, 192, 0.2)',
                'rgba(153, 102, 255, 0.2)',
                'rgba(255, 159, 64, 0.2)'
              ],
              borderColor: [
                'rgba(255, 99, 132, 1)',
                'rgba(54, 162, 235, 1)',
                'rgba(255, 206, 86, 1)',
                'rgba(75, 192, 192, 1)',
                'rgba(153, 102, 255, 1)',
                'rgba(255, 159, 64, 1)'
              ],
              borderWidth: 1
            }]
          },
          options: {
            responsive: true
          }
        });
      }
    });

    return {
      pieChartRef
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
