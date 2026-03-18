<template>
  <div class="bg-gray-950 text-white py-3 px-4 sm:px-6 lg:px-8 border-b border-white/5 relative z-[60]">
    <div class="max-w-7xl mx-auto flex flex-col sm:flex-row justify-between items-center gap-4 text-center sm:text-left">
      <div class="flex flex-col sm:flex-row items-center gap-2 sm:gap-4">
        <span class="bg-orange-600 text-white text-[10px] font-black uppercase tracking-widest px-2 py-0.5 rounded-sm">
          New Resources
        </span>
        <p class="text-sm font-medium text-gray-300">
          Get free resources for your church through <span class="text-white font-bold">Life.Church Open Network</span>.
        </p>
      </div>
      <a href="https://open.life.church/" target="_blank" class="text-xs font-bold uppercase tracking-widest border border-white/20 hover:bg-white hover:text-black hover:border-white px-4 py-2 rounded transition-all duration-300">
        Explore Open Network
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TopBanner'
}
</script>
