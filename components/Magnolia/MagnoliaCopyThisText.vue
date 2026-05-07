<template>
  <div class="text-white/60 text-sm font-medium p-4 bg-white/5 rounded-xl border border-white/10 my-4" v-html="safeContent"></div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  content: String
});

const safeContent = computed(() => window.sanitizeCmsHtml?.(props.content) || '');
</script>
