<template>
  <div class="magnolia-spacer" :class="sizeClass"></div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  size: {
    type: String,
    default: 'pt-normal'
  }
});

const sizeClass = computed(() => {
  // Map Magnolia size strings to UnoCSS classes
  const sizeMap = {
    'pt-none': 'h-0',
    'pt-relaxed': 'h-12 md:h-16',
    'pt-bit_more_relaxed': 'h-16 md:h-24',
    'pt-very_relaxed': 'h-24 md:h-32',
    'pt-even_more_relaxed': 'h-32 md:h-48'
  };
  return sizeMap[props.size] || 'h-8';
});
</script>
