<!-- components/Block/Content.vue -->
<template>
  <section class="py-16">
    <div class="container mx-auto px-4">
      <div class="max-w-4xl mx-auto">
        <h2 v-if="title" class="text-3xl font-bold mb-8">
          {{ title }}
        </h2>
        <div v-if="content" class="prose prose-lg max-w-none">
          <ContentRenderer :value="{ body: parseMarkdown(content) }" />
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { parseMarkdown } from '@nuxt/content/transformers'

defineProps({
  title: String,
  content: String
})
</script>