<template>
  <div class="magnolia-media-collection bg-white py-24">
    <div class="container mx-auto px-6">

      <!-- Latest Collection Hero -->
      <component
        v-if="latest"
        :is="linkComponent(latest)"
        v-bind="linkAttrs(latest)"
        class="block mb-24 relative rounded-3xl overflow-hidden shadow-2xl group cursor-pointer animate-fade-in text-white no-underline"
      >
        <div class="aspect-w-16 aspect-h-7 md:aspect-h-5 bg-gray-900 relative pb-[40%]">
          <img v-if="getImage(latest)" :src="getImage(latest)" class="absolute inset-0 object-cover w-full h-full opacity-80 group-hover:opacity-100 transition-opacity duration-500 transform group-hover:scale-105" alt="Latest Message">
        </div>
        <div class="absolute inset-0 bg-gradient-to-t from-black via-black/50 to-transparent flex flex-col justify-end p-8 md:p-16 pointer-events-none">
          <div class="inline-flex items-center gap-2 text-orange-500 font-bold tracking-widest uppercase text-sm mb-4">
            <span class="w-2 h-2 rounded-full bg-orange-500 animate-pulse"></span>
            Latest Series
          </div>
          <h2 class="text-4xl md:text-6xl font-black text-white mb-4 drop-shadow-lg pointer-events-auto">{{ latest.title || latest.name }}</h2>
          <p class="text-gray-300 text-lg md:text-xl max-w-2xl mb-8 line-clamp-2 md:line-clamp-none pointer-events-auto">{{ latest.description }}</p>
          <div class="flex items-center gap-4 pointer-events-auto">
            <span class="bg-orange-500 group-hover:bg-orange-600 text-white px-8 py-4 rounded-full font-bold transition-transform group-hover:scale-105 flex items-center gap-3">
              <i class="fas fa-play"></i> Watch Now
            </span>
            <span class="text-white/70 font-medium">{{ latest.parts }} Parts</span>
          </div>
        </div>
      </component>

      <!-- Past Collections Grid -->
      <div v-if="past && past.length > 0">
        <h3 class="text-3xl lg:text-4xl font-black mb-12 flex items-center gap-4">
          Past Series
          <div class="h-px bg-gray-200 flex-grow"></div>
        </h3>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <component
            v-for="(item, idx) in past"
            :key="item['@id'] || idx"
            :is="linkComponent(item)"
            v-bind="linkAttrs(item)"
            class="block bg-gray-50 text-gray-950 no-underline rounded-2xl overflow-hidden shadow-sm hover:shadow-xl transition-all duration-300 group cursor-pointer animate-slide-up"
            :style="{ animationDelay: (idx * 100) + 'ms', animationFillMode: 'forwards' }"
          >
            <div class="aspect-w-16 relative bg-gray-200 overflow-hidden pb-[56.25%]">
              <img v-if="getImage(item)" :src="getImage(item)" class="absolute inset-0 object-cover w-full h-full transform transition-transform duration-700 group-hover:scale-110" :alt="item.title || item.name">
            </div>
            <div class="p-8">
              <div class="text-orange-500 text-sm font-bold tracking-wider mb-2 uppercase">{{ item.parts || 'Multiple' }} Parts</div>
              <h4 class="text-2xl font-black mb-3 group-hover:text-orange-500 transition-colors">{{ item.title || item.name }}</h4>
              <p class="text-gray-600 line-clamp-3 mb-6">{{ item.description }}</p>
              <div class="flex items-center text-orange-500 font-bold group-hover:gap-3 transition-all">
                Watch Series <i class="fas fa-arrow-right ml-2 transition-transform group-hover:translate-x-1"></i>
              </div>
            </div>
          </component>
        </div>
      </div>

    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  preload: Object,
  mediaCollectionType: String
});

const latest = computed(() => {
  return props.preload?.latestCollection || null;
});

const past = computed(() => {
  return props.preload?.pastCollections || [];
});

const IMAGE_FIELDS = [
  'landscapeImage_public',
  'cinemaImage_public',
  'superHeroImage_public',
  'albumImage_public',
  'featuredImage_public',
  'image_public',
  'featuredImage',
  'image'
];

const pickImage = (source) => {
  if (!source || typeof source !== 'object') return null;

  for (const field of IMAGE_FIELDS) {
    if (typeof source[field] === 'string' && source[field]) {
      return source[field];
    }
  }

  return null;
};

const getImage = (item) => {
  if (!item) return null;

  if (item.channelImageList) {
    if (Array.isArray(item.channelImageList)) {
      for (const image of item.channelImageList) {
        const resolvedImage = pickImage(image);
        if (resolvedImage) return resolvedImage;
      }
    } else {
      const directImage = pickImage(item.channelImageList);
      if (directImage) return directImage;

      for (const image of Object.values(item.channelImageList)) {
        const resolvedImage = pickImage(image);
        if (resolvedImage) return resolvedImage;
      }
    }
  }

  return pickImage(item);
};

const getUrl = (item) => item?.shareableUrl || item?.openURL || item?.url || '';

const linkComponent = (item) => getUrl(item) ? 'a' : 'div';

const linkAttrs = (item) => {
  const url = getUrl(item);
  return url ? { href: url, target: '_blank', rel: 'noopener noreferrer' } : {};
};
</script>

<style scoped>
.animate-fade-in { animation: fadeIn 1s ease-out forwards; }
.animate-slide-up { opacity: 0; animation: slideUp 0.8s cubic-bezier(0.16, 1, 0.3, 1) forwards; }
@keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
@keyframes slideUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }
.line-clamp-2 { display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; }
.line-clamp-3 { display: -webkit-box; -webkit-line-clamp: 3; -webkit-box-orient: vertical; overflow: hidden; }
</style>
