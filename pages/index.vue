<script setup>
const { data } = await useFetch("/api/tickers/", {
  query: { limit: 15 },
});
</script>
<template>
  <div>
    <h1 class="text-4xl font-bold leading-tight tracking-wide">
      Top Crypto Prices
    </h1>

    <div class="mt-8 overflow-x-auto">
      <table class="w-full">
        <thead class="">
          <tr class="text-xs tracking-wide uppercase border-b border-gray-200">
            <th class="p-4 text-left max-w-10 shrink-0">#</th>
            <th class="p-4 text-left">Currency</th>
            <th class="p-4 text-left">Symbol</th>
            <th class="p-4 text-right">Price (US $)</th>
            <th class="p-4 text-right">&Delta; 1h</th>
            <th class="p-4 text-right">&Delta; 24h</th>
            <th class="p-4 text-right">&Delta; 7d</th>
            <th class="p-4 text-right">Volume - 24h</th>
          </tr>
        </thead>

        <tbody>
          <tr
            v-for="currency in data.data"
            :key="currency.id"
            class="border-b border-gray-200"
          >
            <td class="px-4 py-6 max-w-10">{{ currency.rank }}</td>
            <td class="px-4 py-6">
              <NuxtLink
                :to="'/currency/' + currency.id"
                class="hover:text-teal-600"
                >{{ currency.name }}</NuxtLink
              >
            </td>
            <td class="px-4 py-6">{{ currency.symbol }}</td>
            <td class="px-4 py-6 font-mono text-right">
              {{
                parseFloat(currency.price_usd).toLocaleString(undefined, {
                  minimumFractionDigits: 2,
                })
              }}
            </td>
            <td
              :class="[
                currency.percent_change_1h > 0
                  ? 'text-green-600'
                  : 'text-red-600',
              ]"
              class="px-4 py-6 font-mono text-right"
            >
              {{ currency.percent_change_1h }}%
            </td>
            <td
              :class="[
                currency.percent_change_24h > 0
                  ? 'text-green-600'
                  : 'text-red-600',
              ]"
              class="px-4 py-6 font-mono text-right"
            >
              {{ currency.percent_change_24h }}%
            </td>
            <td
              :class="[
                currency.percent_change_7d > 0
                  ? 'text-green-600'
                  : 'text-red-600',
              ]"
              class="px-4 py-6 font-mono text-right"
            >
              {{ currency.percent_change_7d }}%
            </td>
            <td class="px-4 py-6 font-mono text-right">
              {{ currency.volume24.toLocaleString() }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
