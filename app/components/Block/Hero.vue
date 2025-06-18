<!-- components/Block/Hero.vue -->
<template>
  <section class="bg-gradient-to-r from-blue-600 to-purple-600 text-white py-20">
    <div class="container mx-auto px-4 text-center">
      <h1 v-if="title" class="text-4xl md:text-6xl font-bold mb-6">
        {{ title }}
      </h1>
      <p v-if="description" class="text-xl md:text-2xl mb-8 opacity-90">
        {{ description }}
      </p>
      <div v-if="image" class="mb-8">
        <NuxtImg
            :src="image"
            :alt="title"
            class="mx-auto rounded-lg shadow-lg max-w-md"
        />
      </div>
      <UButton
          v-if="cta"
          :to="cta.href"
          size="lg"
          color="white"
          variant="solid"
      >
        {{ cta.text }}
      </UButton>
    </div>
  </section>
</template>

<script setup>
defineProps({
  title: String,
  description: String,
  image: String,
  cta: Object
})
</script>