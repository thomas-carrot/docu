<template>
  <div class="callout">
    <h2 v-if="$slots.title" class="text-red-600">
      <slot name="title" mdc-unwrap="p" />
    </h2>
    <slot />
  </div>
</template>
