<script setup>
const { data } = await useFetch("https://api.coinlore.net/api/exchanges/");
</script>

<template>
  <div>
    <h1 class="text-4xl font-bold leading-tight tracking-wide">
      Top Cryptocurrency Exchanges
    </h1>
  </div>
</template>
