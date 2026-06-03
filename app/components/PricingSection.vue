<template>
  <section id="pricing" class="bg-blue-900 py-24 px-8">
    <div class="max-w-6xl mx-auto">

      <!-- Section Label -->
      <p class="text-xs uppercase tracking-widest text-gray-300 mb-4">
        Transparent Pricing
      </p>

      <!-- Section Headline -->
      <h2 class="text-5xl font-light uppercase text-gray-300 max-w-lg leading-none mb-16">
        Simple,
        <span class="font-bold italic text-white">honest</span>
        pricing.
      </h2>

      <!-- Pricing Cards -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6">

        <!-- Regular -->
        <div class="bg-gray-300 border border-gray-100 p-10 flex flex-col gap-6">
          <div>
            <p class="text-xs uppercase tracking-widest text-gray-900 mb-2">Regular</p>
            <h3 class="text-5xl font-black text-gray-900">
              Rp 7k
              <span class="text-xl font-light text-gray-900">/kg</span>
            </h3>
          </div>
          <ul class="flex flex-col gap-3">
            <li v-for="item in regular" :key="item"
              class="flex items-center gap-3 text-sm text-gray-900">
              <span class="w-1.5 h-1.5 rounded-full bg-blue-900 shrink-0"></span>
              {{ item }}
            </li>
          </ul>
          <a href="#schedule"
            class="mt-auto border border-gray-900 text-gray-900 text-sm uppercase tracking-widest px-6 py-3 text-center hover:bg-gray-900 hover:text-white transition">
            Order Now
          </a>
        </div>

        <!-- Express -->
        <div class="bg-gray-300 p-10 flex flex-col gap-6">
          <div>
            <p class="text-xs uppercase tracking-widest text-gray-900 mb-2">Express ⚡</p>
            <h3 class="text-5xl font-black text-gray-900">
              Rp 10k
              <span class="text-xl font-light text-gray-900">/kg</span>
            </h3>
          </div>
          <ul class="flex flex-col gap-3">
            <li v-for="item in express" :key="item"
              class="flex items-center gap-3 text-sm text-gray-900">
              <span class="w-1.5 h-1.5 rounded-full bg-blue-900 shrink-0"></span>
              {{ item }}
            </li>
          </ul>
          <a href="#schedule"
            class="mt-auto bg-gray-300 text-gray-900 border border-gray-900 text-sm uppercase tracking-widest px-6 py-3 text-center hover:bg-gray-900 hover:text-white transition">
            Order Express
          </a>
        </div>

      </div>
    </div>
  </section>
</template>

<script setup>
const regular = [
  'Minimum order 2kg',
  'Ready in 2-3 days',
  'Free pickup & delivery',
  'Wash, dry & fold included',
]

const express = [
  'Minimum order 2kg',
  'Ready in 24 hours',
  'Free pickup & delivery',
  'Priority handling',
]
</script>