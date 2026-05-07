<template>
  <div class="border-b border-white/10 group">
    <button
      type="button"
      @click="toggle"
      :aria-expanded="isOpen ? 'true' : 'false'"
      class="w-full flex justify-between items-center py-6 focus:outline-none transition-colors duration-300 group-hover:text-orange-500"
    >
      <h3 class="text-xl font-bold text-left pr-8" v-html="safeTitle"></h3>
      <div
        class="w-8 h-8 rounded-full bg-white/5 flex items-center justify-center transition-transform duration-500"
        :class="{ 'rotate-180 bg-orange-500/20 text-orange-500': isOpen }"
      >
        <i class="fa-solid fa-chevron-down text-sm"></i>
      </div>
    </button>

    <div
      class="overflow-hidden transition-all duration-500 ease-in-out"
      :style="{ maxHeight: isOpen ? '1000px' : '0px', opacity: isOpen ? 1 : 0 }"
    >
      <div class="pb-8 prose prose-invert prose-lg max-w-none text-gray-400 font-light" v-html="safeContent"></div>
    </div>
  </div>
</template>

<script setup>
import { computed, ref, watch } from 'vue';

const props = defineProps({
  title: String,
  content: String,
  isOpened: Boolean
});

const isOpen = ref(props.isOpened || false);
const safeTitle = computed(() => window.sanitizeCmsHtml?.(props.title) || '');
const safeContent = computed(() => window.sanitizeCmsHtml?.(props.content) || '');

const toggle = () => {
  isOpen.value = !isOpen.value;
};

watch(() => props.isOpened, (newVal) => {
  if (newVal !== undefined) isOpen.value = newVal;
});
</script>
