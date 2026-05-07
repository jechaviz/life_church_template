<template>
  <section 
    class="magnolia-single-content-zone relative overflow-hidden" 
    :class="[bgcolor, pyOnMobile, pyOnTabletAndUp, sbOnMobile, sbOnTabletAndUp, alignment, colorsetting]"
    :style="sectionStyle"
  >
    <!-- Background Video -->
    <video 
      v-if="backgroundVideo_public"
      autoplay muted loop playsinline
      class="absolute inset-0 w-full h-full object-cover -z-10 opacity-40"
    >
      <source :src="backgroundVideo_public" type="video/mp4">
    </video>
    <div 
      v-else-if="backgroundImage_public"
      class="absolute inset-0 w-full h-full bg-cover bg-center -z-10"
      :style="{ backgroundImage: `url(${backgroundImage_public})` }"
    ></div>

    <!-- Gradient Overlay -->
    <div 
      v-if="gradientType !== 'none'"
      class="absolute inset-0 -z-5 pointer-events-none"
      :class="gradientClass"
    ></div>

    <div class="container mx-auto px-6 relative z-10">
      <div 
        class="content-wrapper"
        :class="[zoneWidthClass, zoneHeightClass]"
      >
        <MagnoliaZone v-if="zones" :area="zones" area-name="zones" :color-theme="colorTheme" />
      </div>
    </div>
  </section>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  bgcolor: String,
  pyOnMobile: String,
  pyOnTabletAndUp: String,
  sbOnMobile: String,
  sbOnTabletAndUp: String,
  alignment: String,
  colorsetting: String,
  backgroundVideo_public: String,
  backgroundImage_public: String,
  gradientType: {
    type: String,
    default: 'none'
  },
  gradientstart: String,
  gradientend: String,
  zoneWidth: {
    type: String,
    default: 'full-width'
  },
  zoneHeight: String,
  colorTheme: String,
  zones: Object
});

const sectionStyle = computed(() => {
  const styles = {};
  if (props.bgcolor && props.bgcolor.startsWith('#')) {
    styles.backgroundColor = props.bgcolor;
  }
  return styles;
});

const gradientClass = computed(() => {
  if (props.gradientType === 'none') return '';
  if (props.gradientType === 'tb') return 'bg-gradient-to-b from-transparent to-black/60';
  if (props.gradientType === 'lr') return 'bg-gradient-to-r from-black/80 to-transparent';
  return '';
});

const zoneWidthClass = computed(() => {
  if (props.zoneWidth === 'half') return 'max-w-2xl';
  if (props.zoneWidth === 'narrow') return 'max-w-xl mx-auto';
  return 'max-w-none';
});

const zoneHeightClass = computed(() => {
  if (props.zoneHeight === 'tall') return 'min-h-[70vh] flex flex-col justify-center';
  if (props.zoneHeight === 'normal') return 'min-h-[50vh] flex flex-col justify-center';
  return '';
});
</script>
