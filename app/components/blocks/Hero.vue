<template>
  <div class="relative isolate overflow-hidden bg-gray-900 px-6 py-24 sm:py-32 lg:px-8">
    <img
        :src="image "
        :alt="title"
        class="absolute inset-0 -z-10 size-full object-cover"
    >
    <div class="mx-auto max-w-4xl text-center">
      <h1 class="text-5xl font-semibold tracking-tight text-white sm:text-7xl">{{ title || "Commencez la journée du bon pied avec nümorning" }}</h1>
      <p class="mt-8 text-lg font-medium text-pretty text-gray-400 sm:text-xl/8">{{ description || "Produits sains et bio pour un petit-déjeuner gourmand et naturel." }}</p>
    </div>
    <div class="mt-10 flex items-center justify-center gap-x-6">
      <NuxtLink
          :to="cta.href"
          class="rounded-md bg-[#824E1E] px-6 py-3 text-base font-semibold text-white shadow-sm hover:[#824E1E] focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 transition-colors"
      >
        {{ cta.text || "Découvrir les produits" }}
      </NuxtLink>
    </div>
  </div>
</template>

<script setup>
defineProps(['title', 'description', 'image', 'cta', 'type'])
</script>