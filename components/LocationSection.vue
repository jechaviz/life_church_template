<template>
  <section class="relative py-32 bg-[#0a0c10] text-white overflow-hidden">
    <div class="absolute top-0 right-0 w-1/2 h-full bg-orange-600/5 skew-x-12 translate-x-32 pointer-events-none"></div>

    <div class="max-w-7xl mx-auto px-8 sm:px-10 lg:px-12 relative z-10">
      <div class="flex flex-col lg:flex-row items-center gap-16 lg:gap-24">
        <div class="w-full lg:w-1/2 group">
          <div class="relative">
            <div class="absolute -inset-4 border border-white/5 rounded-[32px] transform rotate-2 group-hover:rotate-0 transition-transform duration-700"></div>
            <div class="relative aspect-[4/5] rounded-[28px] overflow-hidden shadow-[0_50px_100px_rgba(0,0,0,0.5)]">
              <img
                src="https://cms-images.life.church/lc-site/pages/who-we-are/Who-We-Are-Desktop-Updated-July2025.jpg"
                alt="People gathered at Life.Church"
                class="w-full h-full object-cover transform scale-105 group-hover:scale-100 transition-transform duration-[2s] ease-out"
              />
              <div class="absolute inset-0 bg-gradient-to-t from-[#0a0c10] via-transparent to-transparent opacity-60"></div>

              <div class="absolute bottom-8 left-8 right-8 p-6 bg-white/8 backdrop-blur-2xl rounded-2xl border border-white/10 flex items-center gap-4">
                <div class="w-12 h-12 bg-orange-600 rounded-xl flex items-center justify-center shadow-lg shadow-orange-600/40">
                  <i class="fa-solid fa-map-pin text-xl"></i>
                </div>
                <div>
                  <p class="text-[10px] uppercase tracking-[0.3em] font-black text-gray-400">Expanding Hope</p>
                  <p class="text-lg font-bold">35+ Campuses Nationwide</p>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="w-full lg:w-1/2 space-y-10">
          <div class="space-y-6">
            <div class="flex items-center gap-4 opacity-60">
              <div class="w-12 h-px bg-white"></div>
              <span class="text-[10px] font-black uppercase tracking-[0.4em]">Near You</span>
            </div>
            <h2 class="text-5xl md:text-7xl font-black leading-[0.9]">
              Find a <span class="text-orange-600">campus.</span>
            </h2>
            <p class="text-xl text-gray-400 leading-relaxed font-light max-w-lg">
              Experience community in person. With locations across the country, there's a place for you to belong.
            </p>
          </div>

          <div class="flex flex-col sm:flex-row gap-4">
            <router-link
              to="/locations"
              class="inline-flex items-center justify-center gap-3 rounded-full bg-white px-8 py-4 text-sm font-black uppercase text-gray-950 hover:bg-orange-600 hover:text-white shadow-2xl shadow-orange-950/40"
            >
              Find a Location
              <i class="fa-solid fa-location-dot text-xs"></i>
            </router-link>
            <a
              href="https://live.life.church/"
              target="_blank"
              rel="noopener noreferrer"
              class="inline-flex items-center justify-center gap-3 rounded-full border border-white/15 px-8 py-4 text-sm font-black uppercase text-white hover:border-orange-600 hover:text-orange-500"
            >
              Church Online
              <i class="fa-solid fa-arrow-up-right-from-square text-xs"></i>
            </a>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'LocationSection'
}
</script>
