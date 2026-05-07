<template>
  <div class="dynamic-page min-h-screen bg-black relative z-[5] overflow-x-hidden pt-32 pb-32 flex flex-col items-center">
    <div v-if="loading" class="flex items-center justify-center min-h-[60vh]">
      <div class="animate-spin rounded-full h-12 w-12 border-t-2 border-b-2 border-orange-500"></div>
    </div>
    
    <div v-else-if="error" class="container mx-auto px-6 py-24 text-center">
      <h1 class="text-4xl font-bold mb-4">Page Not Found</h1>
      <p class="text-white/60 mb-8">We couldn't load the content for this section.</p>
      <router-link to="/" class="px-8 py-3 bg-orange-600 text-white rounded-full font-bold uppercase tracking-widest hover:bg-orange-500 transition-all">
        Back to Home
      </router-link>
    </div>

    <div v-else class="page-content animate-fade-in duration-700">
      <MagnoliaZone v-if="pageData && pageData.main" :area="pageData.main" area-name="main" :color-theme="pageData.colorTheme" />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, watch } from 'vue';

const route = VueRouter.useRoute();
const pageData = ref(null);
const loading = ref(true);
const error = ref(false);

const loadPageData = async () => {
  loading.value = true;
  error.value = false;
  
  // Extract the first part of the path as the page key (e.g., /media -> media)
  const pathParts = route.path.split('/').filter(p => p);
  const pageKey = pathParts[0] || 'index.htm';
  
  try {
    const response = await fetch(`./pages_data/${pageKey}.json`);
    if (!response.ok) throw new Error('Failed to load page data');
    const data = await response.json();
    pageData.value = data.currentPage || data; // Handle both structures
    loading.value = false;
  } catch (err) {
    console.error(`Error loading page ${pageKey}:`, err);
    error.value = true;
    loading.value = false;
  }
};

onMounted(loadPageData);

// Reload data when the route changes (e.g., navigating between subpages)
watch(() => route.path, loadPageData);
</script>

<style scoped>
.animate-fade-in {
  animation: fadeIn 0.8s ease-out forwards;
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(10px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>
