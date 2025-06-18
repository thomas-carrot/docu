<!-- components/DebugInfo.vue -->
<script setup lang="ts">
interface Props {
  data: any
  path: string
  title?: string
}

const props = withDefaults(defineProps<Props>(), {
  title: 'Debug Info'
})

// Récupération sécurisée des blocs avec typage
const blocks = computed(() => {
  const metaBlocks = props.data?.meta?.blocks
  const directBlocks = (props.data as any)?.blocks
  return metaBlocks || directBlocks || []
})
</script>

<template>
  <div class="bg-yellow-100 p-4 mb-4 text-sm border-l-4 border-yellow-500">
    <strong>🐛 {{ title }}:</strong><br>
    Path: {{ path }}<br>
    Page found: {{ !!data }}<br>
    Has meta: {{ !!data?.meta }}<br>
    Has blocks in meta: {{ !!data?.meta?.blocks }}<br>
    Has blocks direct: {{ !!(data as any)?.blocks }}<br>
    Blocks count: {{ blocks.length }}<br>
    Block types: {{ blocks.map((b: any) => b.type).join(', ') }}<br>
    Title: {{ data?.title || data?.meta?.title }}<br>
    Description: {{ data?.description || data?.meta?.description }}<br>

    <details class="mt-2">
      <summary class="cursor-pointer hover:text-yellow-800">🔍 Voir toutes les propriétés de la page</summary>
      <pre class="text-xs mt-2 bg-white p-2 rounded border overflow-auto max-h-96">{{ JSON.stringify(data, null, 2) }}</pre>
    </details>

    <details class="mt-2" v-if="blocks.length > 0">
      <summary class="cursor-pointer hover:text-yellow-800">📦 Détail des blocs</summary>
      <div class="mt-2 space-y-2">
        <div v-for="(block, index) in blocks" :key="index" class="bg-white p-2 rounded border">
          <strong>Bloc {{ index + 1 }}:</strong> {{ (block as any).type }}<br>
          <small class="text-gray-600">{{ Object.keys(block).join(', ') }}</small>
        </div>
      </div>
    </details>
  </div>
</template>