<template>
  <section id="features" class="bg-green-900 py-24 px-6">
    <div class="max-w-6xl mx-auto">

      <!-- Section Header -->
      <div class="text-center mb-16">
        <h2 class="text-3xl font-bold text-white">
          Why choose us?
        </h2>
        <p class="mt-4 text-white max-w-xl mx-auto">
          Everything you need to build and grow your product, 
          all in one place.
        </p>
      </div>

      <!-- Feature Cards -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
        
        <div
          v-for="feature in features"
          :key="feature.title"
          class="bg-yellow-700 rounded-xl p-6 border border-gray-700 hover:border-white transition"
        >
          <div class="text-4xl mb-4">{{ feature.icon }}</div>
          <h3 class="text-xl font-bold text-black mb-2">
            {{ feature.title }}
          </h3>
          <p class="text-black">
            {{ feature.description }}
          </p>
        </div>

      </div>
    </div>
  </section>
</template>

<script setup>
const features = [
  {
    icon: '⚡',
    title: 'Lightning Fast',
    description: 'Optimized for performance so your users get the best experience possible.'
  },
  {
    icon: '🔒',
    title: 'Secure by Default',
    description: 'Built with security best practices so your data stays safe at all times.'
  },
  {
    icon: '📈',
    title: 'Built to Scale',
    description: 'Grows with your business from your first user to your millionth.'
  }
]
</script>