<template>
  <div class="hidden sm:block bg-gray-950 text-white py-2.5 px-6 relative z-[60] overflow-hidden border-b border-white/5">
    <div class="absolute inset-0 bg-gradient-to-r from-orange-600/10 via-transparent to-orange-600/10 opacity-30"></div>
    <div class="max-w-7xl mx-auto flex flex-col sm:flex-row justify-between items-center gap-4 text-center sm:text-left relative z-10">
      <div class="flex items-center gap-6">
        <div class="flex items-center gap-2 group/open cursor-pointer">
           <div class="w-1.5 h-1.5 rounded-full bg-orange-600 animate-pulse"></div>
           <span class="text-[9px] font-black uppercase tracking-[0.3em] text-white/40 group-hover/open:text-orange-500 transition-colors">Open Network</span>
        </div>
        <p class="text-[11px] font-medium text-gray-400 tracking-wide">
          Empowering churches globally with <span class="text-white font-black">100% Free Resources</span>.
        </p>
      </div>
      <a href="https://open.life.church/" target="_blank" rel="noopener noreferrer" class="group flex items-center gap-2 text-[9px] font-black uppercase tracking-[0.3em] text-white/60 hover:text-white transition-all">
        Explore Now
        <i class="fa-solid fa-arrow-right-long text-orange-600 group-hover:translate-x-1 transition-transform"></i>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TopBanner'
}
</script>
