<template>
  <section class="relative isolate overflow-hidden bg-gray-900 px-6 py-24 sm:py-32 lg:px-8">
    <div class="mx-auto max-w-4xl text-center">
      <h1 v-if="$slots.title" class="text-5xl font-semibold tracking-tight text-white sm:text-7xl">
        <slot name="title" />
      </h1>
      <p v-if="$slots.subtitle" class="mt-8 text-lg font-medium text-pretty text-gray-400 sm:text-xl/relaxed">
        <slot name="subtitle" />
      </p>
    </div>
  </section>
</template>
