<template>
  <div class="p-6">
    <h1 class="text-2xl font-bold mb-4">Top 100 Cryptocurrencies</h1>
    <input
      v-model="search"
      type="text"
      placeholder="Search coin..."
      class="mb-4 px-3 py-2 border rounded w-full max-w-md"
    />
    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4">
      <router-link
        v-for="coin in paginatedCoins"
        :key="coin.id"
        :to="`/coin/${coin.id}`"
        class="p-4 border rounded shadow hover:bg-gray-100"
      >
        <div class="flex items-center gap-2">
          <img :src="coin.image" alt="" class="w-6 h-6" />
          <span>{{ coin.name }} ({{ coin.symbol.toUpperCase() }})</span>
        </div>
        <div>Price: ${{ coin.current_price }}</div>
        <div>24h Change: {{ coin.price_change_percentage_24h.toFixed(2) }}%</div>
      </router-link>
    </div>
    <div class="flex justify-center mt-6 gap-2">
      <button
        v-for="page in totalPages"
        :key="page"
        @click="currentPage = page"
        class="px-3 py-1 rounded border"
        :class="{ 'bg-blue-500 text-white': currentPage === page }"
      >
        {{ page }}
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue'
import axios from 'axios'

const coins = ref([])
const search = ref('')
const currentPage = ref(1)
const coinsPerPage = 10

const filteredCoins = computed(() =>
  coins.value.filter(
    (coin: any) =>
      coin.name.toLowerCase().includes(search.value.toLowerCase()) ||
      coin.symbol.toLowerCase().includes(search.value.toLowerCase())
  )
)

const totalPages = computed(() =>
  Math.ceil(filteredCoins.value.length / coinsPerPage)
)

const paginatedCoins = computed(() =>
  filteredCoins.value.slice(
    (currentPage.value - 1) * coinsPerPage,
    currentPage.value * coinsPerPage
  )
)

onMounted(async () => {
  const res = await axios.get('https://api.coingecko.com/api/v3/coins/markets', {
    params: {
      vs_currency: 'usd',
      order: 'market_cap_desc',
      per_page: 100,
      page: 1,
      sparkline: false
    }
  })
  coins.value = res.data
})
</script>