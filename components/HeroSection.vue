<template>
  <section class="relative min-h-[90vh] flex items-center justify-center overflow-hidden bg-gray-900 pt-20">
    <!-- Background Image / Video Wrapper -->
    <div class="absolute inset-0 z-0">
      <!-- Video Background -->
      <video
        autoplay
        muted
        loop
        playsinline
        class="absolute inset-0 w-full h-full object-cover opacity-60"
      >
        <source src="https://cms-assets.life.church/lc-site/pages/easter/Easter Web Background Edit.mp4" type="video/mp4">
      </video>
      <!-- Fallback Image -->
      <img 
        src="https://cms-images.life.church/lc-site/pages/easter/2026/easter-clouds-gradient-lower.jpg" 
        alt="Background" 
        class="absolute inset-0 w-full h-full object-cover transform scale-105 transition-transform duration-[20s] ease-out animate-slow-zoom -z-10"
      />
      <!-- Gradient Overlay matching "black-overlay-50" -->
      <div class="absolute inset-0 bg-gradient-to-t from-gray-900 via-gray-900/40 to-gray-900/20"></div>
    </div>

    <!-- Content Container -->
    <div class="relative z-10 w-full max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-20 flex flex-col md:flex-row items-center justify-between gap-12">
      
      <!-- Left Content Zone -->
      <div class="w-full md:w-1/2 flex flex-col items-center md:items-start text-center md:text-left space-y-8 animate-fade-in-up">
        <!-- Title Image -->
        <img 
          src="https://cms-images.life.church/lc-site/pages/easter/2026/easter-title-full.png" 
          alt="Easter at Life.Church" 
          class="max-w-full w-4/5 md:w-full drop-shadow-2xl translate-y-0 group-hover:-translate-y-2 transition-transform duration-500"
        />
        
        <!-- CTA Button -->
        <a href="https://www.life.church/easter/?utm_source=life_church&utm_medium=homepage&utm_campaign=easter-ad_no-dept_engagement#about" class="btn bg-white/10 hover:bg-white text-white hover:text-gray-900 border border-white/30 hover:border-white backdrop-blur-sm shadow-xl px-8 py-4 text-lg mt-4 animate-fade-in-up animation-delay-300 group">
          Learn What You Can Expect
          <i class="fa-solid fa-arrow-right ml-2 opacity-0 -ml-4 group-hover:opacity-100 group-hover:ml-2 transition-all duration-300"></i>
        </a>
      </div>

      <!-- Right Content Zone -->
      <div class="w-full md:w-1/2 flex flex-col items-center md:items-start text-center md:text-left text-white space-y-6 animate-fade-in-up animation-delay-500">
        <h1 class="text-4xl md:text-6xl font-black tracking-tight text-shadow-md border-b-4 border-orange-500 pb-2 inline-block">
          APRIL 3-6
        </h1>
        <p class="text-xl md:text-2xl font-light text-gray-200 leading-relaxed max-w-lg">
          Find an Easter service time by choosing a Life.Church location near you.
        </p>
        
        <!-- Times/Location Button -->
        <a href="https://www.life.church/locations" class="btn btn-primary shadow-orange-500/50 shadow-lg px-8 py-4 text-lg">
          <i class="fa-solid fa-location-dot mr-2"></i> Find a Location
        </a>
        <p class="text-sm text-gray-400 mt-4">
          All online services are in US Central Time. 
          <a href="https://live.life.church/" class="text-white hover:text-orange-400 font-bold underline transition-colors">Attend Online</a>
        </p>
      </div>

    </div>
  </section>
</template>

<script>
export default {
  name: 'HeroSection'
}
</script>

<style>
@keyframes slowZoom {
  0% { transform: scale(1); }
  100% { transform: scale(1.1); }
}
.animate-slow-zoom {
  animation: slowZoom 30s ease-in-out infinite alternate;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
.animate-fade-in-up {
  animation: fadeInUp 1s ease-out forwards;
  opacity: 0;
}
.animation-delay-300 {
  animation-delay: 0.3s;
}
.animation-delay-500 {
  animation-delay: 0.5s;
}
</style>
