<template>
  <section id="schedule" class="bg-gray-300 py-24 px-8">
    <div class="max-w-6xl mx-auto">

      <!-- Section Label -->
      <p class="text-xs uppercase tracking-widest text-blue-900 mb-4">
        Book a Pickup
      </p>

      <!-- Section Headline -->
      <h2 class="text-5xl font-light uppercase text-gray-900 max-w-lg leading-none mb-16">
        Schedule your
        <span class="font-bold italic text-blue-900">pickup.</span>
      </h2>

      <!-- Form -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-12">

        <!-- Left — Form Fields -->
        <div class="flex flex-col gap-6">

          <!-- Name -->
          <div class="flex flex-col gap-2">
            <label class="text-xs uppercase tracking-widest text-gray-900">Full Name</label>
            <input
              v-model="form.name"
              type="text"
              placeholder="John Doe"
              class="border-b border-gray-900 bg-transparent py-3 text-gray-900 placeholder-blue-900 focus:outline-none focus:border-blue-900 transition"
            />
          </div>

          <!-- Phone -->
          <div class="flex flex-col gap-2">
            <label class="text-xs uppercase tracking-widest text-gray-900">Phone Number</label>
            <input
              v-model="form.phone"
              type="tel"
              placeholder="08xxxxxxxxxx"
              class="border-b border-gray-900 bg-transparent py-3 text-gray-900 placeholder-blue-900 focus:outline-none focus:border-blue-900 transition"
            />
          </div>

          <!-- Address -->
          <div class="flex flex-col gap-2">
            <label class="text-xs uppercase tracking-widest text-gray-900">Pickup Address</label>
            <input
              v-model="form.address"
              type="text"
              placeholder="Jl. Soekarno Hatta No. 1, Malang"
              class="border-b border-gray-900 bg-transparent py-3 text-gray-900 placeholder-blue-900 focus:outline-none focus:border-blue-900 transition"
            />
          </div>

          <!-- Date & Time -->
          <div class="grid grid-cols-2 gap-6">
            <div class="flex flex-col gap-2">
              <label class="text-xs uppercase tracking-widest text-gray-900">Pickup Date</label>
              <input
                v-model="form.date"
                type="date"
                class="border-b border-gray-300 bg-transparent py-3 text-gray-900 focus:outline-none focus:border-blue-900 transition"
              />
            </div>
            <div class="flex flex-col gap-2">
              <label class="text-xs uppercase tracking-widest text-gray-900">Pickup Time</label>
              <select
                v-model="form.time"
                class="border-b border-gray-300 bg-transparent py-3 text-gray-900 focus:outline-none focus:border-blue-900 transition"
              >
                <option value="">Select time</option>
                <option>08:00 - 10:00</option>
                <option>10:00 - 12:00</option>
                <option>13:00 - 15:00</option>
                <option>15:00 - 17:00</option>
              </select>
            </div>
          </div>

          <!-- Service Type -->
          <div class="flex flex-col gap-3">
            <label class="text-xs uppercase tracking-widest text-gray-900">Service Type</label>
            <div class="flex gap-4">
              <button
                v-for="type in ['Regular', 'Express']"
                :key="type"
                @click="form.service = type"
                :class="form.service === type
                  ? 'bg-blue-900 text-white'
                  : 'border border-gray-300 text-gray-900 hover:border-blue-900 hover:text-blue-900'"
                class="text-sm uppercase tracking-widest px-6 py-3 transition"
              >
                {{ type }}
              </button>
            </div>
          </div>

          <!-- Submit -->
          <button
            @click="submitOrder"
            class="mt-4 bg-blue-900 text-white text-sm uppercase tracking-widest px-8 py-4 hover:bg-blue-700 transition w-full"
          >
            Confirm Pickup
          </button>

        </div>

        <!-- Right — Summary -->
        <div class="bg-gray-200 p-10 flex flex-col gap-6 h-fit">
          <p class="text-xs uppercase tracking-widest text-gray-900">Order Summary</p>

          <div class="flex flex-col gap-4">
            <div class="flex justify-between text-sm">
              <span class="text-gray-900 uppercase tracking-widest">Service</span>
              <span class="text-gray-900 font-semibold">{{ form.service || '—' }}</span>
            </div>
            <div class="flex justify-between text-sm">
              <span class="text-gray-900 uppercase tracking-widest">Date</span>
              <span class="text-gray-900 font-semibold">{{ form.date || '—' }}</span>
            </div>
            <div class="flex justify-between text-sm">
              <span class="text-gray-900 uppercase tracking-widest">Time</span>
              <span class="text-gray-900 font-semibold">{{ form.time || '—' }}</span>
            </div>
            <div class="flex justify-between text-sm">
              <span class="text-gray-900 uppercase tracking-widest">Address</span>
              <span class="text-gray-900 font-semibold text-right max-w-[200px]">{{ form.address || '—' }}</span>
            </div>
          </div>

          <div class="border-t border-gray-200 pt-6">
            <div class="flex justify-between">
              <span class="text-xs uppercase tracking-widest text-gray-900">Price per kg</span>
              <span class="text-2xl font-black text-gray-900">
                {{ form.service === 'Express' ? 'Rp 10k' : 'Rp 7k' }}
              </span>
            </div>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>

<script setup>
const supabase = useSupabaseClient()

const form = ref({
  name: '',
  phone: '',
  address: '',
  date: '',
  time: '',
  service: 'Regular'
})

const submitOrder = async () => {
  if (!form.value.name || !form.value.phone || !form.value.address || !form.value.date || !form.value.time) {
    alert('Please fill in all fields')
    return
  }

  const { error } = await supabase
    .from('orders')
    .insert({
      customer_name: form.value.name,
      phone: form.value.phone,
      address: form.value.address,
      pickup_date: form.value.date,
      pickup_time: form.value.time,
      service_type: form.value.service,
      status: 'Order Received'
    })

  if (error) {
    alert('Something went wrong. Please try again.')
    console.error(error)
  } else {
    alert('Order confirmed! We will contact you shortly.')
    form.value = {
      name: '',
      phone: '',
      address: '',
      date: '',
      time: '',
      service: 'Regular'
    }
  }
}
</script>

