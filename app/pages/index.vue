<script setup lang="ts">
const { data: home } = await useAsyncData('home', () =>
    queryCollection('content').path('/pages/').first()
)
definePageMeta({
  layout: 'default'
})


const blocks = home.value?.meta?.blocks || home.value?.blocks || []
const path = '/'
</script>

<template>
  <!-- Debug info temporaire -->
  <div class="bg-yellow-100 p-4 mb-4 text-sm border-l-4 border-yellow-500">
    <strong>🐛 Debug Page Index:</strong><br>
    Path: {{ path }}<br>
    Page found: {{ !!home }}<br>
    Has meta: {{ !!home?.meta }}<br>
    Has blocks in meta: {{ !!home?.meta?.blocks }}<br>
    Has blocks direct: {{ !!home?.blocks }}<br>
    Blocks count: {{ blocks.length }}<br>
    Block types: {{ blocks.map(b => b.type).join(', ') }}<br>
    Title: {{ home?.title || home?.meta?.title }}<br>
    Description: {{ home?.description || home?.meta?.description }}<br>

    <details class="mt-2">
      <summary class="cursor-pointer hover:text-yellow-800">🔍 Voir toutes les propriétés de la page</summary>
      <pre class="text-xs mt-2 bg-white p-2 rounded border overflow-auto max-h-96">{{ JSON.stringify(home, null, 2) }}</pre>
    </details>

    <details class="mt-2" v-if="blocks.length > 0">
      <summary class="cursor-pointer hover:text-yellow-800">📦 Détail des blocs</summary>
      <div class="mt-2 space-y-2">
        <div v-for="(block, index) in blocks" :key="index" class="bg-white p-2 rounded border">
          <strong>Bloc {{ index + 1 }}:</strong> {{ block.type }}<br>
          <small class="text-gray-600">{{ Object.keys(block).join(', ') }}</small>
        </div>
      </div>
    </details>
  </div>

  <!-- Contenu principal -->
  <div v-if="home">
    <ContentRenderer :value="home" />
  </div>
  <div v-else class="bg-red-100 border border-red-400 text-red-700 px-4 py-3 rounded">
    <strong>❌ Erreur:</strong> Home not found - 404
  </div>
</template>