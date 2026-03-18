<template>
  <section class="relative py-24 md:py-32 flex justify-center items-center overflow-hidden">
    <!-- Background Image -->
    <div class="absolute inset-0 z-0">
      <img src="https://cms-images.life.church/lc-site/pages/who-we-are/who-we-are-2025-desktop.jpg" alt="Who we are" class="w-full h-full object-cover" />
      <div class="absolute inset-0 bg-gradient-to-b from-gray-900/60 to-gray-900/80"></div>
    </div>

    <!-- Content Card -->
    <div class="relative z-10 max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center text-white">
      <div class="glass border border-white/20 rounded-3xl p-10 md:p-16 shadow-2xl backdrop-blur-md bg-black/30 hover:bg-black/40 transition-colors duration-500">
        
        <div class="inline-block mb-4 p-3 bg-orange-600/20 rounded-full text-orange-500">
          <i class="fa-solid fa-heart text-3xl"></i>
        </div>

        <h2 class="text-3xl md:text-5xl font-bold tracking-tight mb-6">
          New to Life.Church?
        </h2>
        
        <p class="text-xl md:text-2xl font-light text-gray-200 leading-relaxed mb-10 max-w-2xl mx-auto">
          Here you'll find a safe place to explore your beliefs and connect with others. Wherever you are in life, you're welcome here.
        </p>
        
        <div class="flex flex-col sm:flex-row justify-center items-center gap-4">
          <a href="/who-we-are" class="btn btn-primary w-full sm:w-auto text-lg shadow-orange-600/30">
            Learn More About Us
          </a>
          <a href="https://live.life.church" target="_blank" class="btn bg-white/10 hover:bg-white text-white hover:text-gray-900 border border-white/30 backdrop-blur-sm w-full sm:w-auto text-lg group">
            Attend Life.Church Online
            <i class="fa-solid fa-arrow-up-right-from-square ml-3 text-sm opacity-80 group-hover:text-orange-500 transition-colors"></i>
          </a>
        </div>

      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'WelcomeSection'
}
</script>

<style scoped>
.glass {
  background: rgba(0, 0, 0, 0.2);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
}
</style>
