<template>
  <div class="min-h-screen bg-gray-50">

    <!-- Admin Navbar -->
    <nav class="bg-white border-b border-gray-100 px-8 py-4 flex items-center justify-between">
      <p class="font-black uppercase tracking-widest text-gray-900">
        KilanKiloan <span class="text-blue-800">Admin</span>
      </p>
      <div class="flex items-center gap-6">
        <NuxtLink
          to="/admin/orders"
          class="text-xs uppercase tracking-widest text-gray-500 hover:text-gray-900 transition"
        >
          Orders
        </NuxtLink>
        <button
          @click="signOut"
          class="text-xs uppercase tracking-widest text-red-400 hover:text-red-600 transition"
        >
          Sign Out
        </button>
      </div>
    </nav>

    <!-- Dashboard Content -->
    <div class="max-w-6xl mx-auto px-8 py-12">

      <!-- Welcome -->
      <div class="mb-12">
        <p class="text-xs uppercase tracking-widest text-gray-400 mb-2">Welcome back</p>
        <h1 class="text-4xl font-black uppercase text-gray-900">Dashboard</h1>
      </div>

      <!-- Stats Cards -->
      <div class="grid grid-cols-1 md:grid-cols-4 gap-6 mb-12">
        <div
          v-for="stat in stats"
          :key="stat.label"
          class="bg-white border border-gray-100 p-6"
        >
          <p class="text-xs uppercase tracking-widest text-gray-400 mb-2">{{ stat.label }}</p>
          <p class="text-3xl font-black text-gray-900">{{ stat.value }}</p>
        </div>
      </div>

      <!-- Recent Orders -->
      <div class="bg-white border border-gray-100">
        <div class="px-6 py-4 border-b border-gray-100 flex justify-between items-center">
          <p class="text-xs uppercase tracking-widest text-gray-900 font-black">Recent Orders</p>
          <NuxtLink
            to="/admin/orders"
            class="text-xs uppercase tracking-widest text-blue-800 hover:text-blue-600 transition"
          >
            View All
          </NuxtLink>
        </div>

        <!-- Loading -->
        <div v-if="loading" class="px-6 py-12 text-center">
          <div class="w-6 h-6 border-2 border-blue-800 border-t-transparent rounded-full animate-spin mx-auto"></div>
        </div>

        <!-- Orders Table -->
        <div v-else-if="orders.length > 0" class="overflow-x-auto">
          <table class="w-full">
            <thead>
              <tr class="border-b border-gray-100">
                <th class="text-left px-6 py-3 text-xs uppercase tracking-widest text-gray-400">Customer</th>
                <th class="text-left px-6 py-3 text-xs uppercase tracking-widest text-gray-400">Service</th>
                <th class="text-left px-6 py-3 text-xs uppercase tracking-widest text-gray-400">Pickup Date</th>
                <th class="text-left px-6 py-3 text-xs uppercase tracking-widest text-gray-400">Status</th>
              </tr>
            </thead>
            <tbody>
              <tr
                v-for="order in orders"
                :key="order.id"
                class="border-b border-gray-50 hover:bg-gray-50 transition"
              >
                <td class="px-6 py-4">
                  <p class="text-sm font-semibold text-gray-900">{{ order.customer_name }}</p>
                  <p class="text-xs text-gray-400">{{ order.phone }}</p>
                </td>
                <td class="px-6 py-4 text-sm text-gray-600">{{ order.service_type }}</td>
                <td class="px-6 py-4 text-sm text-gray-600">{{ order.pickup_date }}</td>
                <td class="px-6 py-4">
                  <span
                    :class="{
                      'bg-yellow-50 text-yellow-600': order.status === 'Order Received',
                      'bg-blue-50 text-blue-600': order.status === 'Being Washed',
                      'bg-green-50 text-green-600': order.status === 'Delivered',
                    }"
                    class="text-xs uppercase tracking-widest px-3 py-1"
                  >
                    {{ order.status }}
                  </span>
                </td>
              </tr>
            </tbody>
          </table>
        </div>

        <!-- Empty state -->
        <div v-else class="px-6 py-12 text-center">
          <p class="text-xs uppercase tracking-widest text-gray-300">No orders yet</p>
        </div>

      </div>
    </div>
  </div>
</template>

<script setup>
definePageMeta({
  layout: false
})

const supabase = useSupabaseClient()
const router = useRouter()
const orders = ref([])
const loading = ref(true)

const stats = computed(() => [
  { label: 'Total Orders', value: orders.value.length },
  { label: 'Regular', value: orders.value.filter(o => o.service_type === 'Regular').length },
  { label: 'Express', value: orders.value.filter(o => o.service_type === 'Express').length },
  { label: 'Delivered', value: orders.value.filter(o => o.status === 'Delivered').length },
])

const fetchOrders = async () => {
  loading.value = true
  const { data, error } = await supabase
    .from('orders')
    .select('*')
    .order('created_at', { ascending: false })
    .limit(5)

  if (!error) orders.value = data
  loading.value = false
}

const signOut = async () => {
  await supabase.auth.signOut()
  router.push('/admin/login')
}

onMounted(() => {
  fetchOrders()
})
</script>