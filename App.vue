<template>
  <div class="min-h-screen bg-gray-50 flex flex-col font-sans">
    <TopBanner />
    <AppHeader />
    <main class="flex-grow">
      <HeroSection />
      <!-- Spacer component placeholder -->
      <div class="h-16 lg:h-24"></div>
      <WelcomeSection />
      <!-- Spacer component placeholder -->
      <div class="h-16 lg:h-24"></div>
      <NextStepsSection />
    </main>
    <AppFooter />
  </div>
</template>

<script>
const { loadModule } = window['vue3-sfc-loader'];

export default {
  name: 'App',
  components: {
    TopBanner: Vue.defineAsyncComponent(() => loadModule('./components/TopBanner.vue', options)),
    AppHeader: Vue.defineAsyncComponent(() => loadModule('./components/AppHeader.vue', options)),
    HeroSection: Vue.defineAsyncComponent(() => loadModule('./components/HeroSection.vue', options)),
    WelcomeSection: Vue.defineAsyncComponent(() => loadModule('./components/WelcomeSection.vue', options)),
    NextStepsSection: Vue.defineAsyncComponent(() => loadModule('./components/NextStepsSection.vue', options)),
    AppFooter: Vue.defineAsyncComponent(() => loadModule('./components/AppFooter.vue', options))
  }
}
</script>

<style>
/* Utilities for premium feel */
.glass {
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border-bottom: 1px solid rgba(0, 0, 0, 0.05);
}

.text-shadow-sm {
  text-shadow: 0 1px 2px rgba(0,0,0,0.5);
}

.text-shadow-md {
  text-shadow: 0 2px 4px rgba(0,0,0,0.5);
}

/* Base button styles to be extended by UnoCSS */
.btn {
  @apply inline-flex items-center justify-center font-semibold rounded-full transition-all duration-300;
}
.btn-primary {
  @apply bg-orange-600 text-white hover:bg-orange-700 hover:shadow-lg hover:-translate-y-0.5 px-6 py-3;
}
.btn-secondary {
  @apply bg-white text-gray-900 hover:bg-gray-100 hover:shadow-lg hover:-translate-y-0.5 px-6 py-3 border border-gray-200;
}
</style>
