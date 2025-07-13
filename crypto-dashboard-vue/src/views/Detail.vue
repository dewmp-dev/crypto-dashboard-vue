<template>
  <div class="p-6" v-if="coin">
    <h2 class="text-2xl font-bold mb-2">{{ coin.name }}</h2>
    <div>Market Cap: ${{ coin.market_data.market_cap.usd.toLocaleString() }}</div>
    <div>Total Volume: ${{ coin.market_data.total_volume.usd.toLocaleString() }}</div>
    <div class="mt-6">
      <Line :data="chartData" />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import axios from 'axios'
import { Line } from 'vue-chartjs'
import {
  Chart as ChartJS,
  LineElement,
  CategoryScale,
  LinearScale,
  PointElement
} from 'chart.js'

ChartJS.register(LineElement, CategoryScale, LinearScale, PointElement)

const route = useRoute()
const coin = ref<any>(null)
const chartData = ref<any>(null)

onMounted(async () => {
  const id = route.params.id
  const [coinRes, chartRes] = await Promise.all([
    axios.get(`https://api.coingecko.com/api/v3/coins/${id}`),
    axios.get(`https://api.coingecko.com/api/v3/coins/${id}/market_chart`, {
      params: {
        vs_currency: 'usd',
        days: 7
      }
    })
  ])

  coin.value = coinRes.data
  const prices = chartRes.data.prices.map((p: any) => p[1])
  const labels = chartRes.data.prices.map((p: any) =>
    new Date(p[0]).toLocaleDateString()
  )

  chartData.value = {
    labels,
    datasets: [
      {
        label: 'Price (USD)',
        data: prices,
        borderColor: 'rgba(75,192,192,1)',
        tension: 0.4
      }
    ]
  }
})
</script>