<script setup>
const getIconPath = (iconType) => {
  const icons = {
    location: {
      paths: [
        "M15 10.5a3 3 0 1 1-6 0 3 3 0 0 1 6 0Z",
        "M19.5 10.5c0 7.142-7.5 11.25-7.5 11.25s-7.5-4.108-7.5-11.25a7.5 7.5 0 1 1 15 0Z"
      ]
    },
    email: {
      paths: [
        "M21.75 6.75v10.5a2.25 2.25 0 0 1-2.25 2.25h-15a2.25 2.25 0 0 1-2.25-2.25V6.75m19.5 0A2.25 2.25 0 0 0 19.5 4.5h-15a2.25 2.25 0 0 0-2.25 2.25m19.5 0v.243a2.25 2.25 0 0 1-1.07 1.916l-7.5 4.615a2.25 2.25 0 0 1-2.36 0L3.32 8.91a2.25 2.25 0 0 1-1.07-1.916V6.75"
      ]
    },
    phone: {
      paths: [
        "M2.25 6.75c0 8.284 6.716 15 15 15h2.25a2.25 2.25 0 0 0 2.25-2.25v-1.372c0-.516-.351-.966-.852-1.091l-4.423-1.106c-.44-.11-.902.055-1.173.417l-.97 1.293c-.282.376-.769.542-1.21.38a12.035 12.035 0 0 1-7.143-7.143c-.162-.441.004-.928.38-1.21l1.293-.97c.363-.271.527-.734.417-1.173L6.963 3.102a1.125 1.125 0 0 0-1.091-.852H4.5A2.25 2.25 0 0 0 2.25 4.5v2.25Z"
      ]
    }
  }
  return icons[iconType] || icons.email
}
</script>

<template>
  <div class="bg-white py-24 sm:py-32 pt-16">
    <div class="mx-auto max-w-7xl px-6 lg:px-8">
      <div class="mx-auto max-w-2xl lg:mx-0">
        <h1 v-if="$slots.title" class="text-4xl font-semibold tracking-tight text-pretty text-gray-900 sm:text-5xl">
          <slot name="title" />
        </h1>
        <p v-if="$slots.description" class="mt-6 text-lg/8 text-gray-600">
          <slot name="description" />
        </p>
      </div>
      <div class="mx-auto mt-16 grid max-w-2xl grid-cols-1 gap-8 text-base/7 sm:grid-cols-2 sm:gap-y-16 lg:mx-0 lg:max-w-none lg:grid-cols-3">

        <!-- Adresse -->
        <div v-if="$slots.address_title">
          <h3 class="border-l border-[#824E1E] pl-6 font-semibold text-gray-900 flex items-center gap-3">
            <svg class="h-5 w-5 text-[#824E1E]" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
              <path
                  v-for="(path, index) in getIconPath('location').paths"
                  :key="index"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  :d="path"
              />
            </svg>
            <slot name="address_title" />
          </h3>
          <div v-if="$slots.address_details" class="border-l border-gray-200 pt-2 pl-6 text-gray-600">
            <address class="not-italic">
              <slot name="address_details" />
            </address>
          </div>
        </div>

        <!-- Email -->
        <div v-if="$slots.email_title">
          <h3 class="border-l border-[#824E1E] pl-6 font-semibold text-gray-900 flex items-center gap-3">
            <svg class="h-5 w-5 text-[#824E1E]" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
              <path
                  v-for="(path, index) in getIconPath('email').paths"
                  :key="index"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  :d="path"
              />
            </svg>
            <slot name="email_title" />
          </h3>
          <div v-if="$slots.email_details" class="border-l border-gray-200 pt-2 pl-6 text-gray-600">
            <slot name="email_details" />
          </div>
        </div>

        <!-- Téléphone -->
        <div v-if="$slots.phone_title">
          <h3 class="border-l border-[#824E1E] pl-6 font-semibold text-gray-900 flex items-center gap-3">
            <svg class="h-5 w-5 text-[#824E1E]" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
              <path
                  v-for="(path, index) in getIconPath('phone').paths"
                  :key="index"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  :d="path"
              />
            </svg>
            <slot name="phone_title" />
          </h3>
          <div v-if="$slots.phone_details" class="border-l border-gray-200 pt-2 pl-6 text-gray-600">
            <slot name="phone_details" />
          </div>
        </div>

      </div>
    </div>
  </div>
</template>