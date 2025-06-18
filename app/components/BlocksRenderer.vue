<script setup lang="ts">
import Hero from '~/components/blocks/Hero.vue'

const props = defineProps<{
  blocks: Array<Record<string, any>>
}>()

const componentsMap: Record<string, any> = {
  hero: Hero,
  // etc.
}
</script>

<template>
  <div>
    <div v-for="(block, index) in blocks" :key="`block-${index}-${block.type}`">
      <component
          :is="componentsMap[block.type] || 'div'"
          v-bind="block"
          :data-block-type="block.type"
      />
    </div>

    <p v-if="blocks.length === 0" class="text-center text-gray-500 py-10">
      Aucun bloc de contenu configuré.
    </p>
  </div>
</template>
