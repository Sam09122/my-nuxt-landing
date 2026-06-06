<template>
  <div class="min-h-screen bg-white flex items-center justify-center">
    <div class="text-center">
      <p class="text-xs uppercase tracking-widest text-gray-400 mb-4">
        Authenticating...
      </p>
      <div class="w-8 h-8 border-2 border-blue-800 border-t-transparent rounded-full animate-spin mx-auto"></div>
      <p v-if="errorMsg" class="text-red-500 text-xs mt-4 uppercase tracking-widest">
        {{ errorMsg }}
      </p>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient()
const redirectInfo = useSupabaseCookieRedirect()
const errorMsg = ref('')

onMounted(async () => {
  const code = new URLSearchParams(window.location.search).get('code')

  if (code) {
    const { error } = await supabase.auth.exchangeCodeForSession(code)
    if (error) {
      errorMsg.value = error.message
      setTimeout(() => navigateTo('/admin/login'), 2000)
    } else {
      const path = redirectInfo.pluck()
      navigateTo(path || '/admin')
    }
  } else {
    navigateTo('/admin/login')
  }
})
</script>