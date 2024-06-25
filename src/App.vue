<template>
  <HomeView></HomeView>
  <ChartView>
  </ChartView>
  <PIeView></PIeView>
  <TableView></TableView>
  <ActiveUserChart></ActiveUserChart>
  <RateView></RateView>
</template>

<script lang="ts">

import ChartView from "@/views/ChartView.vue";
import HomeView from "@/views/HomeView.vue";
import PIeView from "@/views/PIeView.vue";
import TableView from "@/views/TableView.vue";
import ActiveUserChart from "@/views/ActiveUserView.vue";
import RateView from "@/views/RateView.vue";





export default {
  name: 'App',
  components: {
    ActiveUserChart,
    ChartView,
    HomeView,
    PIeView,
    TableView,
    RateView
  },
}
</script>
