<template>
  <section class="relative min-h-screen flex flex-col justify-between px-20 pt-28 pb-16 bg-gray-300">

    <!-- Top Content -->
    <div>
        <div class="w-1/2">
            <!-- Top label -->
            <p class="text-xs uppercase tracking-widest text-gray-900 mb-6 font-semibold">
            Laundry Service · Malang
            </p>

            <h1 class="text-5xl md:text-6xl font-light uppercase leading-none text-gray-900">
            Clean clothes,
            <br />
            <span class="font-bold italic text-blue-900">delivered</span>
            <br />
            to your door.
            </h1>

            <p class="mt-8 text-gray-900 font-light text-lg max-w-md leading-relaxed">
            Home laundry service with free pickup and delivery.
            Fresh, clean, and on time — every time.
            </p>

            <div class="mt-10 flex gap-4 flex-wrap">
                <a href="#schedule" class="bg-blue-900 text-white text-sm uppercase tracking-widest px-8 py-4 hover:bg-blue-700 transition">
                    Schedule Pickup
                </a>
                <a href="#how-it-works" class="border border-gray-900 text-gray-900 text-sm uppercase tracking-widest px-8 py-4 hover:bg-gray-900 hover:text-white transition">
                    How It Works
                </a>
            </div>
        </div>
    </div>
    
    <div>
        <!-- Right — Unsplash image -->
        <div class="hidden md:block absolute top-0 right-0 w-1/2 h-full">
        <img
            src="https://images.unsplash.com/photo-1582735689369-4fe89db7114c?w=800&q=80"
            alt="Fresh laundry"
            class="w-full h-full object-cover"
        />
        </div>
    </div>

      

    <!-- Bottom stat bar — unchanged -->
    <div class="flex gap-12 flex-wrap pt-16">
      <div>
        <p class="text-3xl font-black text-gray-900">Rp 7k<span class="text-blue-900">/kg</span></p>
        <p class="text-xs uppercase tracking-widest text-gray-900 font-semibold mt-1">Regular Kiloan</p>
      </div>
      <div>
        <p class="text-3xl font-black text-gray-900">24<span class="text-blue-900">hr</span></p>
        <p class="text-xs uppercase tracking-widest text-gray-900 font-semibold mt-1">Express Available</p>
      </div>
      <div>
        <p class="text-3xl font-black text-gray-900">Free</p>
        <p class="text-xs uppercase tracking-widest text-gray-900 font-semibold mt-1">Pickup & Delivery</p>
      </div>
    </div>

  </section>
</template>











