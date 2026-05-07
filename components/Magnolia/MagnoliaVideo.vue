<template>
  <div class="relative w-full aspect-video rounded-[32px] overflow-hidden shadow-2xl bg-black/50 border border-white/10 group cursor-pointer">
    <iframe v-if="iframeMarkup" :src="iframeSrc" class="w-full h-full border-none" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen></iframe>
    
    <!-- Custom placeholder/poster if no iframe but we have a poster -->
    <div v-if="!iframeMarkup && posterImg" class="absolute inset-0">
      <img :src="posterImg" :alt="posterAlt" class="w-full h-full object-cover opacity-80 group-hover:opacity-100 transition-opacity duration-700" />
      <div class="absolute inset-0 bg-black/30 flex items-center justify-center">
        <div class="w-20 h-20 bg-orange-600/90 rounded-full flex items-center justify-center shadow-[0_0_30px_rgba(234,88,12,0.5)] transform group-hover:scale-110 transition-transform duration-500 backdrop-blur-md">
          <i class="fa-solid fa-play text-white text-2xl ml-1"></i>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  iframeMarkup: String,
  posterImg_public: String,
  posterImg: String,
  posterAlt: String,
  autoStart: Boolean,
  youtubeVideoId: String,
  youtubeID: String,
  videoId: String // Custom life.church video tracking ID
});

// Extract actual src from the iframe markup
const iframeSrc = computed(() => {
  if (!props.iframeMarkup) {
    const yid = props.youtubeID || props.youtubeVideoId || props.videoId;
    if (yid) return `https://www.youtube.com/embed/${yid}?autoplay=${props.autoStart ? 1 : 0}`;
    return '';
  }
  const match = props.iframeMarkup.match(/src="([^"]+)"/);
  return match ? match[1] : '';
});

const posterImg = computed(() => props.posterImg_public || props.posterImg);
</script>
