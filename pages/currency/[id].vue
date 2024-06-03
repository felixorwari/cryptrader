<script setup>
const route = useRoute();
const { data } = await useFetch("/api/ticker/", {
  query: { id: route.params.id },
});
const markets = await useFetch("/api/coin/markets/", {
  query: { id: route.params.id },
});
const coin = data.value[0];
const marketData = markets.data;
</script>

<template>
  <div>
    <h2 class="mb-6 text-4xl font-bold md:text-center">
      {{ coin.name }}
      <span class="text-gray-400">({{ coin.symbol }})</span>
    </h2>

    <!-- Coin Overview -->
    <section class="mt-12">
      <h3 class="my-4 text-2xl font-semibold">Overview</h3>

      <div class="grid border md:grid-cols-2">
        <div class="px-4 py-8 border-b border-gray-200 md:border-r">
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

        <div class="px-4 py-8 border-b border-gray-200">
          <h3
            class="mb-4 text-xs font-medium tracking-wide text-gray-500 uppercase"
          >
            Market Cap
          </h3>

          <div class="flex items-end gap-6">
            <p class="text-2xl">
              ${{ parseFloat(coin.market_cap_usd).toLocaleString() }}
              <span class="text-xs">USD</span>
            </p>

            <span class="text-gray-400"> Rank #{{ coin.rank }} </span>
          </div>
        </div>

        <div class="px-4 py-8 border-b border-gray-200 md:border-r">
          <h3
            class="mb-4 text-xs font-medium tracking-wide text-gray-500 uppercase"
          >
            Trading Volume - 24h
          </h3>

          <p class="text-2xl">
            ${{ coin.volume24.toLocaleString() }}
            <span class="text-xs">USD</span>
          </p>
        </div>

        <div class="px-4 py-8 border-b border-gray-200">
          <h3
            class="mb-4 text-xs font-medium tracking-wide text-gray-500 uppercase"
          >
            Coins Traded
          </h3>

          <p class="text-2xl">
            {{ parseFloat(coin.volume24a).toLocaleString() }}
          </p>
        </div>

        <div
          class="px-4 py-8 border-b border-gray-200 md:border-b-0 md:border-r"
        >
          <h3
            class="mb-4 text-xs font-medium tracking-wide text-gray-500 uppercase"
          >
            Circulating Supply
          </h3>

          <p class="text-2xl">
            {{ parseFloat(coin.csupply).toLocaleString() }}
          </p>
        </div>

        <div class="px-4 py-8 border-b border-gray-200 md:border-b-0">
          <h3
            class="mb-4 text-xs font-medium tracking-wide text-gray-500 uppercase"
          >
            Maximum Supply
          </h3>

          <p v-if="coin.msupply" class="text-2xl">
            {{ parseFloat(coin.msupply).toLocaleString() }}
          </p>
          <p v-else class="text-2xl">Unknown</p>
        </div>
      </div>
    </section>

    <!-- Market Data -->
    <section class="mt-12">
      <h3 class="my-4 text-2xl font-semibold">Top 50 Markets</h3>

      <div class="grid gap-6 sm:grid-cols-2 lg:grid-cols-4">
        <div
          v-for="(market, index) in marketData"
          class="p-4 border rounded-lg shadow-lg shadow-gray-200 hover:scale-[101%] transition-all hover:border-teal-600"
        >
          <h4 class="flex mb-4 font-medium">
            {{ market.name }}
            <span class="inline-block font-normal text-gray-400 ms-auto"
              >#{{ index + 1 }}</span
            >
          </h4>

          <p class="mb-4 text-lg">
            ${{ parseFloat(market.price_usd).toLocaleString() }}
          </p>
          <p class="text-xs text-gray-400 uppercase">
            Coins traded:
            <span class="text-xs text-gray-700">{{
              parseFloat(market.volume).toLocaleString()
            }}</span>
          </p>
        </div>
      </div>
    </section>
  </div>
</template>
