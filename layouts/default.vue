<template>
  <div class="max-w-screen-xl px-4 mx-auto">
    <nav class="flex w-full gap-6 px-4 border-b bg-white/90 backdrop-blur-lg">
      <NuxtLink
        to="#"
        class="py-4 text-2xl font-bold tracking-tight text-gray-500 uppercase pe-4"
        >Cryptrader</NuxtLink
      >
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

    <main class="my-8 min-h-[80vh]">
      <slot />
    </main>

    <footer
      class="sticky top-[100vh] w-full pt-12 mt-40 pb-8 border-t border-gray-200"
    >
      <div class="px-4">
        <p class="text-sm text-gray-400">&copy; 2024 Cryptrader.</p>
      </div>
    </footer>
  </div>
</template>
