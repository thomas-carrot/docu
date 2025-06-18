<script setup lang="ts">
const { data: home } = await useAsyncData('home', () =>
    queryCollection('content').path('/pages/').first()
)
definePageMeta({
  layout: 'default'
})
</script>

<template>

  <!-- debug -->
  <DebugInfo :data="home" path="/" title="coucou" :display="false" />

  <!-- Contenu principal -->
  <div v-if="home">
    <BlocksRenderer :blocks="(home as any)?.blocks || (home as any)?.meta?.blocks || []" />
  </div>
  <div v-else class="bg-red-100 border border-red-400 text-red-700/50 px-4 py-3 rounded">
    <p>Erreur: Home not found - 404</p>
  </div>
</template>