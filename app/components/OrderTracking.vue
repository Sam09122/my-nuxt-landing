<template>
  <section id="track" class="bg-blue-900 py-24 px-8">
    <div class="max-w-6xl mx-auto">

      <!-- Section Label -->
      <p class="text-xs uppercase tracking-widest text-white mb-4">
        Track Your Order
      </p>

      <!-- Section Headline -->
      <h2 class="text-5xl font-light uppercase text-white max-w-lg leading-none mb-16">
        Where are
        <span class="font-bold italic text-gray-200">your clothes?</span>
      </h2>

      <!-- Search Bar -->
      <div class="flex gap-4 mb-16 max-w-lg">
        <input
          v-model="orderId"
          type="text"
          placeholder="Enter your order ID"
          class="flex-1 border-b border-gray-300 bg-transparent py-3 text-white placeholder-gray-300 focus:outline-none focus:border-gray-900 transition"
        />
        <button
          @click="trackOrder"
          class="bg-gray-900 text-white text-sm uppercase tracking-widest px-6 py-3 hover:bg-gray-300 hover:text-gray-900 transition-colors"
        >
          Track
        </button>
      </div>

      <!-- Status Timeline -->
      <div v-if="tracked" class="max-w-2xl">

        <!-- Order Info -->
        <div class="flex justify-between items-center mb-10 pb-6 border-b border-gray-100">
          <div>
            <p class="text-xs uppercase tracking-widest text-white">Order ID</p>
            <p class="text-lg font-black text-white mt-1">{{ orderId }}</p>
          </div>
          <div class="text-right">
            <p class="text-xs uppercase tracking-widest text-white">Service</p>
            <p class="text-lg font-black text-white mt-1">Regular Kiloan</p>
          </div>
          <div class="text-right">
            <p class="text-xs uppercase tracking-widest text-white">Est. Delivery</p>
            <p class="text-lg font-black text-white mt-1">Tomorrow, 3PM</p>
          </div>
        </div>

        <!-- Timeline Steps -->
        <div class="flex flex-col gap-0">
          <div
            v-for="(step, index) in steps"
            :key="step.label"
            class="flex gap-6 items-start"
          >
            <!-- Left — dot and line -->
            <div class="flex flex-col items-center">
              <div
                :class="index <= currentStep
                  ? 'bg-black border-gray-900'
                  : 'bg-white border-gray-200'"
                class="w-4 h-4 rounded-full border-2 shrink-0 mt-1"
              ></div>
              <div
                v-if="index < steps.length - 1"
                :class="index < currentStep ? 'bg-white' : 'bg-gray-100'"
                class="w-0.5 h-12"
              ></div>
            </div>

            <!-- Right — content -->
            <div class="pb-8">
              <p
                :class="index <= currentStep ? 'text-white' : 'text-gray-300'"
                class="text-sm uppercase tracking-widest font-black"
              >
                {{ step.label }}
              </p>
              <p
                :class="index <= currentStep ? 'text-white' : 'text-gray-200'"
                class="text-sm mt-1"
              >
                {{ step.description }}
              </p>
              <p v-if="index <= currentStep" class="text-xs text-white mt-1 uppercase tracking-widest">
                {{ step.time }}
              </p>
            </div>
          </div>
        </div>

      </div>

      <!-- Empty state -->
      <div v-else class="text-gray-300 text-sm uppercase tracking-widest">
        Enter your order ID above to track your laundry.
      </div>

    </div>
  </section>
</template>

<script setup>
const orderId = ref('')
const tracked = ref(false)
const currentStep = ref(2)

const steps = [
  { label: 'Order Received', description: 'Your order has been confirmed.', time: 'Today, 9:00 AM' },
  { label: 'Picked Up', description: 'Your laundry has been collected.', time: 'Today, 10:30 AM' },
  { label: 'Being Washed', description: 'Your clothes are currently being washed.', time: 'Today, 12:00 PM' },
  { label: 'Ready for Delivery', description: 'Clean and folded, out for delivery soon.', time: '' },
  { label: 'Delivered', description: 'Your laundry has been delivered.', time: '' },
]

const trackOrder = () => {
  if (orderId.value.trim()) {
    tracked.value = true
  }
}
</script>