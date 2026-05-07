<template>
  <section class="relative min-h-[92vh] flex items-end overflow-hidden bg-gray-950 pt-28 sm:pt-36">
    <div class="absolute inset-0">
      <picture>
        <source
          media="(max-width: 640px)"
          srcset="https://cms-images.life.church/lc-site/pages/who-we-are/Who-We-Are-Mobile-Update-July2025.jpg"
        />
        <img
          src="https://cms-images.life.church/lc-site/pages/who-we-are/Who-We-Are-Desktop-Updated-July2025.jpg"
          alt="People gathered at Life.Church"
          class="w-full h-full object-cover"
        />
      </picture>
      <div class="absolute inset-0 bg-gradient-to-r from-gray-950 via-gray-950/70 to-gray-950/20"></div>
      <div class="absolute inset-0 bg-gradient-to-t from-gray-950 via-transparent to-gray-950/30"></div>
    </div>

    <div class="relative z-10 w-full max-w-7xl mx-auto px-6 sm:px-8 lg:px-10 pb-20 sm:pb-28">
      <div class="max-w-3xl text-white">
        <p class="text-sm font-black uppercase text-orange-500 mb-6">Life.Church Online and in person</p>
        <h1 class="text-5xl sm:text-7xl lg:text-8xl font-black leading-[0.9] mb-8">
          You're welcome here.
        </h1>
        <p class="text-lg sm:text-2xl text-white/80 leading-relaxed max-w-2xl mb-10">
          Find community, watch the latest message, and take your next step with Life.Church.
        </p>

        <div class="flex flex-col sm:flex-row gap-4 mb-12">
          <router-link
            to="/locations"
            class="inline-flex items-center justify-center px-8 py-4 bg-orange-600 text-white rounded-full font-black hover:bg-orange-500 shadow-2xl shadow-orange-600/30"
          >
            Find a Location
          </router-link>
          <a
            href="https://live.life.church/"
            target="_blank"
            rel="noopener noreferrer"
            class="inline-flex items-center justify-center px-8 py-4 bg-white text-gray-950 rounded-full font-black hover:bg-gray-100"
          >
            Watch Online
            <i class="fa-solid fa-arrow-up-right-from-square text-xs ml-3"></i>
          </a>
        </div>

        <div class="grid grid-cols-3 gap-4 max-w-xl">
          <div v-for="stat in stats" :key="stat.label" class="border-t border-white/20 pt-4">
            <div class="text-2xl sm:text-3xl font-black">{{ stat.value }}</div>
            <div class="text-xs text-white/60 font-bold uppercase mt-1">{{ stat.label }}</div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'HeroSection',
  data() {
    return {
      stats: [
        { value: '35+', label: 'Campuses' },
        { value: '24/7', label: 'Online' },
        { value: 'Free', label: 'Resources' }
      ]
    }
  }
}
</script>
