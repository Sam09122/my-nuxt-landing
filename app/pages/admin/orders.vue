<template>
  <div class="min-h-screen bg-gray-50">

    <!-- Admin Navbar -->
    <nav class="bg-white border-b border-gray-100 px-8 py-4 flex items-center justify-between">
      <NuxtLink to="/admin" class="font-black uppercase tracking-widest text-gray-900">
        KilanKiloan <span class="text-blue-800">Admin</span>
      </NuxtLink>
      <div class="flex items-center gap-6">
        <NuxtLink
          to="/admin/orders"
          class="text-xs uppercase tracking-widest text-blue-800"
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

    <!-- Content -->
    <div class="max-w-6xl mx-auto px-8 py-12">

      <!-- Header -->
      <div class="flex justify-between items-start mb-12">
        <div>
          <p class="text-xs uppercase tracking-widest text-gray-400 mb-2">Manage</p>
          <h1 class="text-4xl font-black uppercase text-gray-900">All Orders</h1>
        </div>
        <!-- Filter -->
        <select
          v-model="statusFilter"
          class="border border-gray-200 bg-white px-4 py-2 text-xs uppercase tracking-widest text-gray-600 focus:outline-none focus:border-blue-800"
        >
          <option value="">All Status</option>
          <option>Order Received</option>
          <option>Picked Up</option>
          <option>Being Washed</option>
          <option>Ready for Delivery</option>
          <option>Delivered</option>
        </select>
      </div>

      <!-- Loading -->
      <div v-if="loading" class="py-12 text-center">
        <div class="w-6 h-6 border-2 border-blue-800 border-t-transparent rounded-full animate-spin mx-auto"></div>
      </div>

      <!-- Orders Table -->
      <div v-else class="bg-white border border-gray-100">
        <table class="w-full">
          <thead>
            <tr class="border-b border-gray-100">
              <th class="text-left px-6 py-3 text-xs uppercase tracking-widest text-gray-400">Customer</th>
              <th class="text-left px-6 py-3 text-xs uppercase tracking-widest text-gray-400">Address</th>
              <th class="text-left px-6 py-3 text-xs uppercase tracking-widest text-gray-400">Service</th>
              <th class="text-left px-6 py-3 text-xs uppercase tracking-widest text-gray-400">Pickup Date</th>
              <th class="text-left px-6 py-3 text-xs uppercase tracking-widest text-gray-400">Time</th>
              <th class="text-left px-6 py-3 text-xs uppercase tracking-widest text-gray-400">Status</th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="order in filteredOrders"
              :key="order.id"
              class="border-b border-gray-50 hover:bg-gray-50 transition"
            >
              <td class="px-6 py-4">
                <p class="text-sm font-semibold text-gray-900">{{ order.customer_name }}</p>
                <p class="text-xs text-gray-400">{{ order.phone }}</p>
              </td>
              <td class="px-6 py-4 text-sm text-gray-600 max-w-[200px]">{{ order.address }}</td>
              <td class="px-6 py-4 text-sm text-gray-600">{{ order.service_type }}</td>
              <td class="px-6 py-4 text-sm text-gray-600">{{ order.pickup_date }}</td>
              <td class="px-6 py-4 text-sm text-gray-600">{{ order.pickup_time }}</td>
              <td class="px-6 py-4">
                <select
                  :value="order.status"
                  @change="updateStatus(order.id, $event.target.value)"
                  class="text-xs uppercase tracking-widest border border-gray-200 px-3 py-1 focus:outline-none focus:border-blue-800 bg-white"
                >
                  <option>Order Received</option>
                  <option>Picked Up</option>
                  <option>Being Washed</option>
                  <option>Ready for Delivery</option>
                  <option>Delivered</option>
                </select>
              </td>
            </tr>
          </tbody>
        </table>

        <!-- Empty state -->
        <div v-if="filteredOrders.length === 0" class="px-6 py-12 text-center">
          <p class="text-xs uppercase tracking-widest text-gray-300">No orders found</p>
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
const statusFilter = ref('')

const filteredOrders = computed(() => {
  if (!statusFilter.value) return orders.value
  return orders.value.filter(o => o.status === statusFilter.value)
})

const fetchOrders = async () => {
  loading.value = true
  const { data, error } = await supabase
    .from('orders')
    .select('*')
    .order('created_at', { ascending: false })

  if (!error) orders.value = data
  loading.value = false
}

const updateStatus = async (id, newStatus) => {
  const { error } = await supabase
    .from('orders')
    .update({ status: newStatus })
    .eq('id', id)

  if (!error) {
    const order = orders.value.find(o => o.id === id)
    if (order) order.status = newStatus
  }
}

const signOut = async () => {
  await supabase.auth.signOut()
  router.push('/admin/login')
}

onMounted(() => {
  fetchOrders()
})
</script>