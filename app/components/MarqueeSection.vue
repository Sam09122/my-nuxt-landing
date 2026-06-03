<template>
  <div class="bg-blue-900 py-4 overflow-hidden whitespace-nowrap">
    <div class="animate-marquee inline-flex gap-12">
      <span v-for="i in 3" :key="i" class="inline-flex gap-12">
        <span class="text-white text-sm uppercase tracking-widest font-medium">Pickup & Delivery</span>
        <span class="text-white">·</span>
        <span class="text-white text-sm uppercase tracking-widest font-medium">Regular Kiloan</span>
        <span class="text-white">·</span>
        <span class="text-white text-sm uppercase tracking-widest font-medium">Express 24hr</span>
        <span class="text-white">·</span>
        <span class="text-white text-sm uppercase tracking-widest font-medium">Rp 7.000/kg</span>
        <span class="text-white">·</span>
        <span class="text-white text-sm uppercase tracking-widest font-medium">Free Pickup</span>
        <span class="text-white">·</span>
      </span>
    </div>
  </div>
</template>

<style scoped>
.animate-marquee {
  animation: marquee 30s linear infinite;
}

@keyframes marquee {
  0% { transform: translateX(0); }
  100% { transform: translateX(-33.33%); }
}
</style>