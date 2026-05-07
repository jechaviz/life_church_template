<template>
  <section class="relative py-32 overflow-hidden bg-white">
    <!-- Sophisticated Background Pattern -->
    <div class="absolute inset-0 opacity-[0.03] pointer-events-none">
      <div class="absolute inset-0" style="background-image: radial-gradient(#000 1px, transparent 1px); background-size: 40px 40px;"></div>
    </div>

    <!-- Floating Glass Island -->
    <div class="relative max-w-5xl mx-auto px-6 sm:px-8">
      <div class="relative group">
        <!-- Animated Glow behind the card -->
        <div class="absolute -inset-1 bg-gradient-to-r from-orange-600 to-yellow-500 rounded-[40px] blur-2xl opacity-20 group-hover:opacity-40 transition-opacity duration-1000"></div>

        <div class="relative bg-white border border-gray-100 rounded-[40px] shadow-[0_50px_100px_-20px_rgba(0,0,0,0.1)] overflow-hidden flex flex-col items-center text-center p-12 sm:p-20 space-y-12">

          <!-- Icon Badge -->
          <div class="w-20 h-20 bg-orange-50 rounded-3xl flex items-center justify-center text-orange-600 transform -rotate-6 group-hover:rotate-0 transition-transform duration-700 shadow-inner">
            <i class="fa-solid fa-heart text-3xl"></i>
          </div>

          <div class="space-y-6 max-w-2xl">
            <h2 class="text-5xl sm:text-7xl font-black text-gray-900 tracking-[-0.05em] leading-[0.9]">
              New to <span class="text-orange-600 italic">Life.Church?</span>
            </h2>
            <p class="text-xl sm:text-2xl font-light text-gray-500 leading-relaxed">
              Whether you’re just starting to ask questions or looking for a place to belong, we’re here to help you find your next step.
            </p>
          </div>

          <div class="flex flex-col sm:flex-row items-center gap-6 pt-4">
            <router-link to="/who-we-are" class="btn-premium-dark px-10 py-5 bg-gray-900 text-white rounded-full text-[12px] font-black uppercase tracking-[0.3em] hover:bg-orange-600 shadow-2xl transition-all duration-500">
              Learn More About Us
            </router-link>
            <a href="https://live.life.church/" target="_blank" rel="noopener noreferrer" class="flex items-center gap-3 text-[12px] font-black uppercase tracking-[0.3em] text-gray-400 hover:text-orange-600 transition-colors group/link">
              Attend Online
              <i class="fa-solid fa-up-right-from-square text-[10px] group-hover:translate-y-[-2px] group-hover:translate-x-[2px] transition-transform"></i>
            </a>
          </div>

          <!-- Subtle Background Text -->
          <span class="absolute right-[-5%] bottom-[-10%] text-[150px] font-black text-gray-50/50 leading-none select-none pointer-events-none">HOME</span>
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
