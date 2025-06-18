<!-- components/DebugInfo.vue -->
<script setup lang="ts">
interface Props {
  data: any
  path: string
  title?: string
  display?: boolean
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
  <div v-if="display" class="bg-yellow-100 p-4 mb-4 text-sm border-l-4 border-yellow-500">
    <strong>🐛 Title :  {{ title }}</strong><br>
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
      <div class="mt-2 space-y-4">
        <div
            v-for="(block, index) in blocks"
            :key="index"
            class="bg-white p-4 rounded-xl border shadow-sm"
        >
          <p class="text-sm font-semibold text-gray-700 mb-2">
            Bloc {{ index + 1 }} – <span class="text-blue-600">{{ block.type }}</span>
          </p>

          <div class="text-sm text-gray-800 space-y-1">
            <div
                v-for="(value, key) in block"
                :key="key"
                class="flex flex-wrap gap-1"
            >
              <span class="font-medium text-gray-600">{{ key }}:</span>
              <span class="break-all">
            {{
                  typeof value === 'object'
                      ? JSON.stringify(value)
                      : value
                }}
          </span>
            </div>
          </div>
        </div>
      </div>
    </details>
  </div>
</template>