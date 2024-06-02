<script setup>
const route = useRoute();
const { data } = await useFetch("/api/ticker/", {
  query: { id: route.params.id },
});
const { markets } = await useFetch("/api/coin/markets/", {
  query: { id: route.params.id },
});
const coin = data.value[0];
</script>

<template>
  <div>
    <h2 class="mb-6 text-2xl font-bold">
      {{ coin.name }}
      <span class="text-xs text-gray-500">({{ coin.symbol }})</span>
    </h2>

    <div class="grid border-t md:grid-cols-2">
      <div class="px-4 py-8 border-b border-gray-200 md:border-r">
        <h3
          class="mb-4 text-xs font-medium tracking-wide text-gray-500 uppercase"
        >
          Rank
        </h3>

        <p class="text-lg">{{ coin.rank }}</p>
      </div>

      <div class="px-4 py-8 border-b border-gray-200">
        <h3
          class="mb-4 text-xs font-medium tracking-wide text-gray-500 uppercase"
        >
          Live Price
        </h3>

        <div class="flex items-end gap-6">
          <p class="text-4xl">
            ${{ parseFloat(coin.price_usd).toLocaleString() }}
            <span class="text-xs">USD</span>
          </p>

          <span
            :class="[
              coin.percent_change_24h > 0 ? 'text-green-600' : 'text-red-600',
            ]"
            ><span v-if="coin.percent_change_24h > 0">+</span
            >{{ coin.percent_change_24h }}%</span
          >
        </div>
      </div>

      <div class="px-4 py-8 border-b border-gray-200 md:border-r">
        <h3
          class="mb-4 text-xs font-medium tracking-wide text-gray-500 uppercase"
        >
          Market Cap
        </h3>

        <p class="text-lg">
          ${{ parseFloat(coin.market_cap_usd).toLocaleString() }}
          <span class="text-xs">USD</span>
        </p>
      </div>

      <div class="px-4 py-8 border-b border-gray-200">
        <h3
          class="mb-4 text-xs font-medium tracking-wide text-gray-500 uppercase"
        >
          Trading Volume - 24h
        </h3>

        <p class="text-lg">
          ${{ coin.volume24.toLocaleString() }}
          <span class="text-xs">USD</span>
        </p>
      </div>

      <div class="px-4 py-8 border-b border-gray-200 md:border-r">
        <h3
          class="mb-4 text-xs font-medium tracking-wide text-gray-500 uppercase"
        >
          Total Supply
        </h3>

        <p class="text-lg">{{ parseFloat(coin.tsupply).toLocaleString() }}</p>
      </div>

      <div class="px-4 py-8 border-b border-gray-200">
        <h3
          class="mb-4 text-xs font-medium tracking-wide text-gray-500 uppercase"
        >
          Circulating Supply
        </h3>

        <p class="text-lg">{{ parseFloat(coin.csupply).toLocaleString() }}</p>
      </div>

      <div class="px-4 py-8 border-b border-gray-200">
        <h3
          class="mb-4 text-xs font-medium tracking-wide text-gray-500 uppercase"
        >
          Coins Traded
        </h3>

        <p class="text-lg">{{ parseFloat(coin.volume24a).toLocaleString() }}</p>
      </div>
    </div>
  </div>
</template>
