<template>
  <div class="p-4">
    <button
      @click="goBack"
      class="mb-4 px-4 py-2 bg-gray-200 rounded hover:bg-gray-300 text-sm">
      ← Back
    </button>

    <div v-if="coinData">
      <h1 class="text-xl font-bold mb-2">{{ coinData.name }} ({{ coinData.symbol.toUpperCase() }})</h1>
      <img :src="coinData.image.large" alt="logo" class="w-20 h-20" />
      <p>Market Cap: ${{ coinData.market_data.market_cap.usd.toLocaleString() }}</p>
      <p>Total Volume: ${{ coinData.market_data.total_volume.usd.toLocaleString() }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import axios from 'axios'

const route = useRoute()
const router = useRouter()
const coinId = route.params.id as string

const coinData = ref<any>(null)

onMounted(async () => {
  const response = await axios.get(
    `https://api.coingecko.com/api/v3/coins/${coinId}`
  )
  coinData.value = response.data
})

function goBack() {
  router.back()
}
</script>
