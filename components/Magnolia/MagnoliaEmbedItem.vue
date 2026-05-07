<template>
  <div class="w-full overflow-hidden" :class="[alignmentClass, widthClass]" v-html="safeEmbedCode"></div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  embedCode: String,
  alignment: String,
  maxWidth: String
});

const alignmentClass = computed(() => {
  if (props.alignment === 'center') return 'mx-auto';
  if (props.alignment === 'right') return 'ml-auto';
  return '';
});

const widthClass = computed(() => {
  if (props.maxWidth) return `max-w-[${props.maxWidth}px]`;
  return 'max-w-full';
});

const safeEmbedCode = computed(() => {
  return window.sanitizeCmsHtml?.(props.embedCode, { allowIframes: true }) || '';
});
</script>
