<template>
  <div :class="[containerClasses]">
    <img 
      v-if="src"
      :src="src" 
      :alt="altText"
      :class="[imgClasses]"
      :style="customStyle"
      loading="lazy"
    />
  </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  image_public: String,
  largeImage_public: String,
  image: Object,
  alt: String,
  alignment: String,
  imgWidth: String, // 'full-width' or specific like '150'
  maxwidth: String,
  sbOnMobile: String,
  sbOnTabletAndUp: String
});

const src = computed(() => {
  return props.largeImage_public || props.image_public || (props.image && props.image['@link']) || null;
});

const altText = computed(() => props.alt || 'Life.Church Image');

const containerClasses = computed(() => {
  const classes = ['relative', 'flex', 'w-full'];
  
  if (props.alignment === 'center') classes.push('justify-center');
  if (props.alignment === 'text-left' || props.alignment === 'left') classes.push('justify-start');
  if (props.alignment === 'text-right' || props.alignment === 'right') classes.push('justify-end');
  
  if (props.sbOnMobile && props.sbOnMobile !== 'mb-none') classes.push(props.sbOnMobile);
  if (props.sbOnTabletAndUp && props.sbOnTabletAndUp !== 'mb-none') classes.push(`md:${props.sbOnTabletAndUp}`);
  
  return classes.join(' ');
});

const imgClasses = computed(() => {
  const classes = ['object-contain', 'transition-opacity', 'duration-500'];
  if (props.imgWidth === 'full-width') {
    classes.push('w-full');
  }
  return classes.join(' ');
});

const customStyle = computed(() => {
  if (props.maxwidth && props.imgWidth !== 'full-width') {
    return { maxWidth: `${props.maxwidth}px`, width: '100%' };
  }
  return {};
});
</script>
