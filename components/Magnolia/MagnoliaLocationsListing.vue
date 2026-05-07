<template>
  <div class="magnolia-locations-listing">
    <div class="container mx-auto px-6 py-24">
      <div class="text-center max-w-3xl mx-auto mb-16 animate-fade-in">
        <div class="flex items-center justify-center gap-3 mb-6 opacity-0 animate-slide-up" style="animation-delay: 100ms; animation-fill-mode: forwards;">
          <div class="h-px w-8 bg-orange-500"></div>
          <span class="text-orange-500 font-bold uppercase tracking-widest text-sm">{{ churchOnline || 'Locations' }}</span>
          <div class="h-px w-8 bg-orange-500"></div>
        </div>

        <h2 class="text-5xl md:text-6xl font-black mb-6 tracking-tight opacity-0 animate-slide-up" style="animation-delay: 200ms; animation-fill-mode: forwards;">
          {{ headingText || 'One church in multiple locations' }}
        </h2>
      </div>

      <!-- Reuse our premium LocationSection content layout! -->
      <LocationSection />

      <div v-if="url && linklabel" class="mt-16 text-center opacity-0 animate-slide-up" style="animation-delay: 500ms; animation-fill-mode: forwards;">
        <a :href="url" target="_blank" rel="noopener noreferrer" class="inline-flex items-center px-8 py-4 bg-white/5 hover:bg-white/10 text-white rounded-full font-bold uppercase tracking-widest transition-all duration-300 hover:scale-105 active:scale-95 border border-white/10 hover:border-orange-500/50 group">
          {{ linklabel }}
          <i class="fas fa-arrow-right ml-3 text-orange-500 group-hover:translate-x-1 transition-transform"></i>
        </a>
      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  headingText: String,
  churchOnline: String,
  url: String,
  linklabel: String
});
</script>

<style scoped>
.animate-fade-in { animation: fadeIn 1s ease-out forwards; }
.animate-slide-up { animation: slideUp 0.8s cubic-bezier(0.16, 1, 0.3, 1) forwards; }
@keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
@keyframes slideUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }
</style>
