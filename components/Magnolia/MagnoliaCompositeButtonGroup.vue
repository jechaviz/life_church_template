<template>
  <div
    class="magnolia-composite-button-group flex flex-wrap gap-4"
    :class="[alignment, sbOnMobile, sbOnTabletAndUp]"
  >
    <template v-for="(item, key) in buttonItems" :key="key">
      <a
        v-if="isExternal(item.url)"
        :href="getRoute(item.url)"
        target="_blank"
        rel="noopener noreferrer"
        class="inline-flex items-center px-8 py-4 rounded-full font-bold uppercase tracking-widest transition-all duration-300"
        :class="[
          item.style === 'btn-primary'
            ? (colorTheme === 'green' ? 'bg-[#00a859]' : 'bg-orange-600') + ' text-white hover:opacity-90 hover:scale-105 active:scale-95 shadow-lg shadow-black/10'
            : (colorTheme === 'green' ? 'border-[#00a859]/40 hover:bg-[#00a859]/10 text-[#00a859]' : 'border-white/20 hover:bg-white/10 text-white') + ' backdrop-blur-md hover:scale-105 active:scale-95 border'
        ]"
      >
        {{ item.text }}
        <i v-if="item.icon && item.icon.icon" :class="['fas', `fa-${item.icon.icon}`, 'ml-3']"></i>
      </a>
      <router-link
        v-else
        :to="getRoute(item.url)"
        class="inline-flex items-center px-8 py-4 rounded-full font-bold uppercase tracking-widest transition-all duration-300"
        :class="[
          item.style === 'btn-primary'
            ? (colorTheme === 'green' ? 'bg-[#00a859]' : 'bg-orange-600') + ' text-white hover:opacity-90 hover:scale-105 active:scale-95 shadow-lg shadow-black/10'
            : (colorTheme === 'green' ? 'border-[#00a859]/40 hover:bg-[#00a859]/10 text-[#00a859]' : 'border-white/20 hover:bg-white/10 text-white') + ' backdrop-blur-md hover:scale-105 active:scale-95 border'
        ]"
      >
        {{ item.text }}
        <i v-if="item.icon && item.icon.icon" :class="['fas', `fa-${item.icon.icon}`, 'ml-3']"></i>
      </router-link>
    </template>
  </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  items: Object,
  alignment: String,
  sbOnMobile: String,
  sbOnTabletAndUp: String,
  colorTheme: String
});

const buttonItems = computed(() => {
  return normalizeItems(props.items);
});

const normalizeItems = (source) => {
  if (!source || typeof source !== 'object') return [];

  const keys = Array.isArray(source['@nodes']) && source['@nodes'].length
    ? source['@nodes']
    : Object.keys(source).filter(key => /^\d+$/.test(key)).sort((a, b) => parseInt(a, 10) - parseInt(b, 10));

  return keys
    .map(key => source[key])
    .filter(item => item && typeof item === 'object' && item.text);
};

const isExternal = (url) => {
  if (!url) return false;
  return /^(https?:)?\/\//.test(url) || /^(mailto|tel):/.test(url);
};

const getRoute = (url) => {
  if (!url) return '/';
  if (isExternal(url)) {
     if (url.startsWith('/')) return 'https://www.life.church' + url;
     return url;
  }
  return url.replace('https://www.life.church', '');
};
</script>
