<template>
  <div class="chart-container">
    <h5 class="text-center mb-3">Twubric Score Distribution</h5>
    <canvas ref="chartCanvas"></canvas>
  </div>
</template>

<script setup>
import { onMounted, ref, watch } from 'vue'
import { Chart, registerables } from 'chart.js'
Chart.register(...registerables)

const props = defineProps({ users: Array })
const chartCanvas = ref(null)
let chartInstance = null

function prepareChartData(users) {
  return {
    labels: users.map((u) => u.fullname),
    datasets: [
      {
        label: 'Total Twubric Score',
        data: users.map((u) => u.twubric.total),
        backgroundColor: 'rgba(54, 162, 235, 0.5)',
        borderColor: 'rgba(54, 162, 235, 1)',
        borderWidth: 1
      }
    ]
  }
}

onMounted(() => {
  const ctx = chartCanvas.value.getContext('2d')
  chartInstance = new Chart(ctx, {
    type: 'bar',
    data: prepareChartData(props.users),
    options: {
      responsive: true,
      plugins: {
        legend: { display: false },
        tooltip: { mode: 'index', intersect: false }
      },
      scales: {
        y: {
          beginAtZero: true,
          title: {
            display: true,
            text: 'Score'
          }
        }
      }
    }
  })
})

watch(
  () => props.users,
  (newUsers) => {
    if (chartInstance) {
      chartInstance.data = prepareChartData(newUsers)
      chartInstance.update()
    }
  }
)
</script>

<style scoped>
.chart-container {
  background-color: #fff;
  padding: 1.5rem;
  border-radius: 12px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
  margin-bottom: 2rem;
}
canvas {
  max-width: 100%;
  height: 400px;
}
</style>
