<template>
  <main>
    <HeroSection />

    <!-- Overlapping Section Transition -->
    <div class="relative z-20 -mt-20">
      <WelcomeSection />
    </div>

    <div class="h-16 md:h-24"></div>

    <LocationSection />

    <div class="h-16 md:h-24"></div>

    <MediaSection />

    <div class="h-16 md:h-24"></div>

    <NextStepsSection />

    <div class="h-16 md:h-24"></div>
  </main>
</template>

<script>
const { loadModule } = window['vue3-sfc-loader'];
const sfcOptions = window.sfcOptions;
const loadAsyncComponent = (path) => Vue.defineAsyncComponent(() => loadModule(path, sfcOptions));

export default {
  name: 'Home',
  components: {
    HeroSection: loadAsyncComponent('./components/HeroSection.vue'),
    WelcomeSection: loadAsyncComponent('./components/WelcomeSection.vue'),
    LocationSection: loadAsyncComponent('./components/LocationSection.vue'),
    MediaSection: loadAsyncComponent('./components/MediaSection.vue'),
    NextStepsSection: loadAsyncComponent('./components/NextStepsSection.vue')
  }
}
</script>

<style>
/* Utilities for premium feel remain global or in App.vue */
.glass {
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border-bottom: 1px solid rgba(0, 0, 0, 0.05);
}

.text-shadow-sm { text-shadow: 0 1px 2px rgba(0,0,0,0.5); }
.text-shadow-md { text-shadow: 0 2px 4px rgba(0,0,0,0.5); }

.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  font-weight: 600;
  border-radius: 9999px;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}
.btn-primary {
  background-color: var(--lc-orange);
  color: white;
  padding: 0.75rem 1.5rem;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
}
.btn-primary:hover {
  background-color: var(--lc-orange-dark);
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
  transform: translateY(-2px);
}
</style>
