<!-- components/Block/Contact.vue -->
<template>
  <section class="py-16 bg-gray-50">
    <div class="container mx-auto px-4">
      <h2 v-if="title" class="text-3xl font-bold text-center mb-12">
        {{ title }}
      </h2>
      <div class="max-w-2xl mx-auto grid md:grid-cols-3 gap-8 text-center">
        <div v-if="email" class="p-6">
          <UIcon name="heroicons:envelope" class="text-3xl text-blue-600 mb-4 mx-auto" />
          <h3 class="font-semibold mb-2">Email</h3>
          <a :href="`mailto:${email}`" class="text-blue-600 hover:underline">
            {{ email }}
          </a>
        </div>
        <div v-if="phone" class="p-6">
          <UIcon name="heroicons:phone" class="text-3xl text-blue-600 mb-4 mx-auto" />
          <h3 class="font-semibold mb-2">Téléphone</h3>
          <a :href="`tel:${phone}`" class="text-blue-600 hover:underline">
            {{ phone }}
          </a>
        </div>
        <div v-if="address" class="p-6">
          <UIcon name="heroicons:map-pin" class="text-3xl text-blue-600 mb-4 mx-auto" />
          <h3 class="font-semibold mb-2">Adresse</h3>
          <p class="text-gray-600">{{ address }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
defineProps({
  title: String,
  email: String,
  phone: String,
  address: String
})
</script>