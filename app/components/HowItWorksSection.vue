<template>
  <section id="how-it-works" class="bg-gray-300 py-24 px-8">
    <div class="max-w-6xl mx-auto">

      <!-- Section Label -->
      <p class="text-lg uppercase tracking-widest text-blue-900 mb-1">
        The Process
      </p>

      <!-- Section Headline -->
      <h2 class="text-5xl font-light uppercase text-gray-900 max-w-lg leading-none border-b border-gray-900 py-6 my-0">
        How it
        <span class="font-bold italic text-blue-900">works.</span>
      </h2>

      <!-- Steps -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-0">

        <div
          v-for="(step, index) in steps"
          :key="step.title"
          class="py-12 pr-12"
        >
          <!-- Step Number -->
          <p class="text-6xl font-black text-blue-900 mb-6 leading-none">
            0{{ index + 1 }}
          </p>

          <!-- Icon -->
          <p class="text-3xl mb-4">{{ step.icon }}</p>

          <!-- Title -->
          <h3 class="text-xl font-black uppercase text-gray-900 mb-3">
            {{ step.title }}
          </h3>

          <!-- Description -->
          <p class="text-gray-900 leading-relaxed text-sm">
            {{ step.description }}
          </p>
        </div>

      </div>
    </div>
  </section>
</template>

<script setup>
const steps = [
  {
    icon: '📅',
    title: 'Schedule Pickup',
    description: 'Book a pickup time that works for you. We\'ll come to your door to collect your laundry.'
  },
  {
    icon: '🧺',
    title: 'We Wash & Dry',
    description: 'Your clothes are washed, dried, and folded with care using quality detergents.'
  },
  {
    icon: '🚚',
    title: 'We Deliver',
    description: 'Clean, fresh laundry delivered back to your door within 24-48 hours.'
  }
]
</script>