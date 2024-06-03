<script setup>
const { data } = await useFetch("/api/exchanges/");
const exchanges = data.value;
</script>

<template>
  <div>
    <h1 class="text-4xl font-bold leading-tight tracking-wide">
      Top Crypto Exchanges
    </h1>

    <div class="mt-8 overflow-x-auto">
      <table class="w-full">
        <thead class="">
          <tr class="text-xs tracking-wide uppercase border-b border-gray-200">
            <th class="p-4 text-xs text-left uppercase">ID</th>
            <th class="p-4 text-xs text-left uppercase">Exchange</th>
            <th class="p-4 text-xs text-left uppercase">Country</th>
            <th class="p-4 text-xs text-right uppercase">Volume (US $)</th>
            <th class="p-4 text-xs text-right uppercase">Active Pairs</th>
            <th class="p-4 text-xs text-left uppercase">Link</th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="exchange in exchanges"
            :key="exchange.key"
            class="border-b border-gray-200"
          >
            <td class="px-4 py-6">{{ exchange.id }}</td>
            <td class="px-4 py-6">{{ exchange.name }}</td>
            <td class="px-4 py-6">{{ exchange.country }}</td>
            <td class="px-4 py-6 font-mono text-right">
              {{ parseFloat(exchange.volume_usd).toLocaleString() }}
            </td>
            <td class="px-4 py-6 font-mono text-right">
              {{ exchange.active_pairs.toLocaleString() }}
            </td>
            <td class="px-4 py-6">
              <NuxtLink
                target="_blank"
                :to="exchange.url"
                class="hover:text-teal-600 hover:underline"
                >{{ exchange.url }}</NuxtLink
              >
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
