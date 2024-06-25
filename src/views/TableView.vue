<template>
  <div>
    <table>
      <thead>
      <tr>
        <th>Month</th>
        <th>Value</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="(value, index) in tableData" :key="index">
        <td>{{ tableLabels[index] }}</td>
        <td>{{ value }}</td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from 'vue';

export default defineComponent({
  name: 'TableView',
  setup() {
    const tableLabels = ref<string[]>([]);
    const tableData = ref<number[]>([]);

    onMounted(async () => {
      const response = await fetch('http://localhost:8000/api/fake-data');
      const data = await response.json();
      tableLabels.value = data.barChart.labels;
      tableData.value = data.barChart.data;
    });

    return {
      tableLabels,
      tableData
    };
  }
});
</script>

<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
  margin: 20px 0;
}

th, td {
  padding: 12px;
  border: 1px solid #ddd;
}

th {
  background-color: #f4f4f4;
}
</style>
