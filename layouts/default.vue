<template>
  <div class="max-w-screen-xl px-4 mx-auto">
    <header class="sticky top-0 z-50">
      <nav
        class="flex items-center w-full gap-6 px-4 border-b bg-white/70 backdrop-blur"
      >
        <div
          class="flex items-center text-2xl font-bold tracking-tight text-gray-500 lowercase"
        >
          <img src="/assets/logo.png" class="max-h-[35px] w-auto" /><span
            class="sr-only"
            >Cryptrader</span
          >
        </div>
        <NuxtLink
          to="/"
          exactActiveClass="border-teal-600 text-teal-600"
          class="px-4 py-4 font-semibold tracking-wide transition-all border-b-2 border-transparent hover:text-teal-600"
          >Currencies</NuxtLink
        >
        <NuxtLink
          to="/exchanges"
          exactActiveClass="border-teal-600 text-teal-600"
          class="px-4 py-4 font-semibold tracking-wide transition-all border-b-2 border-transparent hover:text-teal-600"
          >Exchanges</NuxtLink
        >
      </nav>
    </header>

    <main class="my-8 min-h-[80vh]">
      <slot />

      <p class="mt-12 text-sm italic text-gray-500 transition-all">
        Data from
        <NuxtLink
          to="https://www.coinlore.com/cryptocurrency-data-api"
          target="_blank"
          class="underline hover:text-teal-600 hover:underline-offset-4"
          >CoinLore</NuxtLink
        >
        API
      </p>
    </main>

    <footer class="w-full pt-12 pb-8 mt-40 border-t border-gray-200">
      <div class="px-4">
        <p class="text-sm text-gray-400">&copy; 2024 Cryptrader.</p>
      </div>
    </footer>
  </div>
</template>

<style>
.page-enter-active,
.page-leave-active {
  transition: all 0.4s;
}
.page-enter-from,
.page-leave-to {
  opacity: 0;
  filter: blur(1rem);
}
</style>
