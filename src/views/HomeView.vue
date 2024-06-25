<template>
  <div>
    <Doughnut
        id="my-chart-id2"
        :data="chartData"
        :options="chartOptions" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from 'vue';
import { Doughnut } from 'vue-chartjs';
import { Chart as ChartJS, Title, Tooltip, Legend, ArcElement, CategoryScale, LinearScale } from 'chart.js';

ChartJS.register(Title, Tooltip, Legend, ArcElement, CategoryScale, LinearScale);

export default defineComponent({
  name: 'DoughnutChart',
  components: { Doughnut },
  setup() {
    const chartData = ref({
      labels: ['Online', 'On the Spot', 'Other', 'Telephone'],
      datasets: [
        {
          backgroundColor: ['#4186b8', '#51ace4', '#00D8FF', '#2a16dd'],
          data: [50, 20, 20, 10]
        }
      ]
    });

    const chartOptions = ref({
      responsive: true,
      maintainAspectRatio: false
    });

    onMounted(async () => {
      const response = await fetch('http://localhost:8000/api/fake-data');
      const data = await response.json();
      chartData.value = {
        labels: data.pieChart.labels,
        datasets: [
          {
            backgroundColor: ['#4186b8', '#51ace4', '#00D8FF', '#2a16dd'],
            data: data.pieChart.data
          }
        ]
      };
    });

    return {
      chartData,
      chartOptions
    };
  }
});
</script>

<style scoped>
.Barre {
  margin-top: -300px;
  margin-right: 510px;
}
</style>
