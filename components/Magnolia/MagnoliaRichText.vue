<template>
  <div
    class="magnolia-richtext prose prose-invert max-w-none mb-6"
    :class="[alignment, colorsetting, sbOnMobile, sbOnTabletAndUp]"
    v-html="safeContent"
  ></div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  content: String,
  alignment: {
    type: String,
    default: 'text-left'
  },
  colorsetting: String,
  sbOnMobile: String,
  sbOnTabletAndUp: String
});

const safeContent = computed(() => window.sanitizeCmsHtml?.(props.content) || '');
</script>

<style scoped>
.magnolia-richtext :deep(p) {
  margin-bottom: 1.25rem;
  line-height: 1.75;
}
.magnolia-richtext :deep(a) {
  color: var(--lc-orange, #ff5a00);
  text-decoration: underline;
  transition: opacity 0.2s;
}
.magnolia-richtext :deep(a:hover) {
  opacity: 0.8;
}
</style>
