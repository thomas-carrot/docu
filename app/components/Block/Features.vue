<!-- components/Block/Features.vue -->
<template>
  <section class="py-16">
    <div class="container mx-auto px-4">
      <h2 v-if="title" class="text-3xl font-bold text-center mb-12">
        {{ title }}
      </h2>
      <div class="grid md:grid-cols-3 gap-8" v-if="items">
        <div
            v-for="(item, index) in items"
            :key="index"
            class="text-center p-6 rounded-lg border border-gray-200 hover:shadow-lg transition-shadow"
        >
          <UIcon
              v-if="item.icon"
              :name="item.icon"
              class="mx-auto text-4xl text-blue-600 mb-4"
          />
          <h3 class="text-xl font-semibold mb-3">{{ item.title }}</h3>
          <p class="text-gray-600">{{ item.description }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
defineProps({
  title: String,
  items: Array
})
</script>