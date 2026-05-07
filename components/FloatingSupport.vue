<template>
  <div class="hidden sm:block fixed bottom-8 right-8 z-[100] group">
    <!-- Tooltip -->
    <div class="absolute bottom-full right-0 mb-4 opacity-0 group-hover:opacity-100 transition-all duration-300 transform translate-y-2 group-hover:translate-y-0 pointer-events-none">
      <div class="bg-gray-900 text-white text-xs font-bold uppercase tracking-widest px-4 py-2 rounded-lg shadow-2xl whitespace-nowrap">
        Need Help?
      </div>
      <!-- Triangle -->
      <div class="w-3 h-3 bg-gray-900 rotate-45 mx-auto -mt-1.5 mr-6 shadow-2xl"></div>
    </div>

    <!-- Floating Button -->
    <router-link to="/contact" aria-label="Contact Life.Church support" class="w-14 h-14 bg-orange-600 text-white rounded-full shadow-2xl shadow-orange-600/40 flex items-center justify-center hover:bg-orange-500 hover:scale-110 active:scale-95 transition-all duration-300 relative">
      <i class="fa-solid fa-comment-dots text-2xl"></i>
      <!-- Pulse Effect -->
      <span class="absolute inset-0 rounded-full bg-orange-600 animate-ping opacity-20"></span>
    </router-link>
  </div>
</template>

<script>
export default {
  name: 'FloatingSupport'
}
</script>
