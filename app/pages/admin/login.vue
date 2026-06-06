<template>
  <div class="min-h-screen bg-gray-50 flex items-center justify-center px-8">
    <div class="w-full max-w-md">

      <!-- Logo -->
      <div class="text-center mb-12">
        <p class="text-2xl font-black uppercase tracking-widest text-gray-900">
          KilanKiloan
        </p>
        <p class="text-xs uppercase tracking-widest text-gray-400 mt-2">
          Admin Dashboard
        </p>
      </div>

      <!-- Login Form -->
      <div class="bg-white p-10 border border-gray-100">

        <h1 class="text-2xl font-black uppercase text-gray-900 mb-8">
          Sign In
        </h1>

        <!-- Error Message -->
        <div v-if="error" class="bg-red-50 border border-red-200 text-red-600 text-sm px-4 py-3 mb-6 uppercase tracking-widest">
          {{ error }}
        </div>

        <div class="flex flex-col gap-6">

          <!-- Email -->
          <div class="flex flex-col gap-2">
            <label class="text-xs uppercase tracking-widest text-gray-400">
              Email
            </label>
            <input
              v-model="email"
              type="email"
              placeholder="admin@kilankiloan.com"
              class="border-b border-gray-300 bg-transparent py-3 text-gray-900 placeholder-gray-300 focus:outline-none focus:border-blue-800 transition"
            />
          </div>

          <!-- Password -->
          <div class="flex flex-col gap-2">
            <label class="text-xs uppercase tracking-widest text-gray-400">
              Password
            </label>
            <input
              v-model="password"
              type="password"
              placeholder="••••••••"
              class="border-b border-gray-300 bg-transparent py-3 text-gray-900 placeholder-gray-300 focus:outline-none focus:border-blue-800 transition"
            />
          </div>

          <!-- Submit -->
          <button
            @click="signIn"
            :disabled="loading"
            class="bg-blue-800 text-white text-sm uppercase tracking-widest px-8 py-4 hover:bg-blue-700 transition disabled:opacity-50 disabled:cursor-not-allowed"
          >
            {{ loading ? 'Signing in...' : 'Sign In' }}
          </button>

        </div>

        <p class="text-xs text-gray-400 mt-6 text-center">
          Admin access only.
        </p>

      </div>

    </div>
  </div>
</template>

<script setup>
definePageMeta({
  layout: false
})

const supabase = useSupabaseClient()
const email = ref('')
const password = ref('')
const loading = ref(false)
const error = ref('')

const signIn = async () => {
  if (!email.value || !password.value) {
    error.value = 'Please enter your email and password'
    return
  }

  loading.value = true
  error.value = ''

  const { error: signInError } = await supabase.auth.signInWithPassword({
    email: email.value,
    password: password.value,
  })

  loading.value = false

  if (signInError) {
    error.value = signInError.message
  } else {
    navigateTo('/admin')
  }
}
</script>