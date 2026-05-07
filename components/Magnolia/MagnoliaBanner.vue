<template>
  <div class="w-full bg-gradient-to-r from-orange-600 to-yellow-500 p-8 rounded-3xl shadow-2xl border border-white/20 relative overflow-hidden group">
    <div class="absolute inset-0 bg-[url('https://www.transparenttextures.com/patterns/cubes.png')] opacity-10 mix-blend-overlay"></div>
    <div class="relative z-10 flex flex-col md:flex-row items-center justify-between gap-8">
      <div class="flex-1 space-y-4">
        <h3 v-if="headingText" class="text-3xl font-black text-white leading-tight uppercase tracking-tight">{{ headingText }}</h3>
        <div v-if="safeContent" class="text-white/90 font-medium text-lg leading-relaxed" v-html="safeContent"></div>
      </div>
      <div>
        <slot name="buttonGroup"></slot>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  headingText: String,
  content: String,
  bgcolor: String
});

const safeContent = computed(() => window.sanitizeCmsHtml?.(props.content) || '');
</script>
