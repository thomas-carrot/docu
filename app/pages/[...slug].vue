<script setup lang="ts">
const route = useRoute()
const path = route.path

const { data: page } = await useAsyncData(`content-${path}`, () =>
    queryCollection('content').path(`/pages${path}/`).first()
)

if (!page.value) {
  throw createError({ statusCode: 404, statusMessage: 'Page not found' })
}

const layoutToUse = page.value?.meta?.layout || 'default'

onMounted(() => {
  if (layoutToUse !== 'default') {
    setPageLayout(layoutToUse)
  }
})
</script>

<template>
  <div>
    <ContentRenderer v-if="page" :value="page" />
  </div>
</template>