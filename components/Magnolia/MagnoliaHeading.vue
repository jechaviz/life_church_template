<template>
  <div 
    class="magnolia-heading" 
    :class="[alignment, colorsetting, sbOnMobile, sbOnTabletAndUp]"
  >
    <component 
      :is="headingLevel" 
      :class="headingTypeClasses"
      v-html="safeHeadingText"
    >
    </component>
  </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  headingText: String,
  headingLevel: {
    type: String,
    default: 'h2'
  },
  headingType: {
    type: String,
    default: 'section_header'
  },
  alignment: {
    type: String,
    default: 'text-left'
  },
  colorsetting: {
    type: String,
    default: 'currentColor'
  },
  sbOnMobile: String,
  sbOnTabletAndUp: String
});

const headingTypeClasses = computed(() => {
  const types = {
    'huge': 'text-6xl md:text-8xl font-black tracking-tighter leading-none mb-4',
    'section_header': 'text-4xl md:text-5xl font-bold tracking-tight mb-2',
    'group_header': 'text-xl md:text-2xl font-bold uppercase tracking-widest mb-4 opacity-80',
    'subhead': 'text-2xl md:text-3xl font-semibold mb-4',
    'body': 'text-lg md:text-xl font-normal opacity-90'
  };
  return types[props.headingType] || types.section_header;
});

const safeHeadingText = computed(() => window.sanitizeCmsHtml?.(props.headingText) || '');
</script>
