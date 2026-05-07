<template>
  <div v-if="contentItems.length || headingText" class="magnolia-content-list my-8">
    <div v-if="headingText || viewAllLink" class="flex flex-col sm:flex-row sm:items-end sm:justify-between gap-4 mb-8">
      <h3 v-if="headingText" class="text-2xl md:text-3xl font-black tracking-tight">
        {{ headingText }}
      </h3>
      <component
        v-if="viewAllLink"
        :is="linkComponent(viewAllLink)"
        v-bind="linkAttrs(viewAllLink)"
        class="inline-flex items-center text-sm font-bold text-orange-500 hover:text-orange-400 uppercase"
      >
        View All
        <i class="fas fa-arrow-right ml-2 text-xs"></i>
      </component>
    </div>

    <div
      v-if="contentItems.length"
      :class="isCarousel ? 'flex overflow-x-auto gap-6 pb-8 snap-x no-scrollbar' : 'grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8'"
    >
      <component
        v-for="item in contentItems"
        :key="item['@id'] || item.id || item.title"
        :is="cardComponent(item)"
        v-bind="cardAttrs(item)"
        :class="[
          isCarousel ? 'flex-shrink-0 w-72 md:w-96 snap-start' : '',
          'group/card block rounded-2xl overflow-hidden bg-white text-gray-950 no-underline shadow-lg border border-black/5 transition-all duration-300 hover:-translate-y-1 hover:shadow-2xl'
        ]"
      >
        <div v-if="getImage(item)" class="aspect-video relative overflow-hidden bg-gray-100">
          <img
            :src="getImage(item)"
            :alt="getTitle(item)"
            class="w-full h-full object-cover transition-transform duration-700 group-hover/card:scale-105"
          />
        </div>

        <div class="p-6 md:p-8">
          <p v-if="getEyebrow(item)" class="text-xs font-black text-orange-600 uppercase mb-3">
            {{ getEyebrow(item) }}
          </p>
          <h4 class="text-xl md:text-2xl font-black mb-4 leading-tight">
            {{ getTitle(item) }}
          </h4>
          <div
            v-if="item.content"
            class="content-copy text-gray-600 leading-relaxed"
            v-html="safeHtml(item.content)"
          ></div>
          <p v-else-if="item.subTitle || item.description" class="text-gray-600 leading-relaxed">
            {{ item.subTitle || item.description }}
          </p>

          <span
            v-if="getItemUrl(item)"
            class="inline-flex items-center mt-6 text-sm font-black text-orange-600 uppercase"
          >
            {{ item.linkTitle || item.linkLabel || item.buttonName || 'Learn More' }}
            <i class="fas fa-arrow-right ml-2 text-xs transition-transform group-hover/card:translate-x-1"></i>
          </span>
        </div>
      </component>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  headingText: String,
  viewAllLink: String,
  type: Object,
  preload: Object,
  items: Object,
  itemsType: String
});

const isCarousel = computed(() => {
  const layoutType = props.itemsType || props.type?.itemsType || props.type?.field || '';
  return String(layoutType).includes('carousel');
});

const contentItems = computed(() => {
  const source = props.preload?.items || props.items;
  return normalizeItems(source);
});

const normalizeItems = (source) => {
  if (!source || typeof source !== 'object') return [];

  const keys = Array.isArray(source['@nodes']) && source['@nodes'].length
    ? source['@nodes']
    : Object.keys(source).filter(key => /^\d+$/.test(key)).sort((a, b) => parseInt(a, 10) - parseInt(b, 10));

  return keys
    .map(key => ({ ...source[key], id: key }))
    .filter(item => item && typeof item === 'object' && (item.title || item.name || item.content));
};

const getTitle = (item) => item.title || item.name || 'Life.Church';

const getEyebrow = (item) => {
  return item.partNumber ? `Episode ${item.partNumber}` : item.label || item.category || '';
};

const getImage = (item) => {
  if (!item) return '';
  return item.largeImage_public
    || item.image_public
    || item.featuredImage_public
    || item.largeImage?.['@link']
    || item.image?.['@link']
    || item.image
    || '';
};

const getItemUrl = (item) => {
  if (!item || item.wholeCardLink === 'false') return '';
  return item.url || item.link || item.linkUrl || '';
};

const isExternalUrl = (url) => /^(https?:)?\/\//.test(url) || /^(mailto|tel):/.test(url);

const normalizeRoute = (url) => {
  if (!url) return '/';

  try {
    const parsed = new URL(url);
    if (parsed.hostname === 'www.life.church' || parsed.hostname === 'life.church') {
      return parsed.pathname.replace(/\/$/, '') || '/';
    }
  } catch (err) {
    // Relative routes fall through unchanged.
  }

  return url;
};

const linkComponent = (url) => isExternalUrl(normalizeRoute(url)) ? 'a' : 'router-link';

const linkAttrs = (url) => {
  const route = normalizeRoute(url);
  return isExternalUrl(route)
    ? { href: route, target: '_blank', rel: 'noopener noreferrer' }
    : { to: route };
};

const cardComponent = (item) => {
  const url = getItemUrl(item);
  if (!url) return 'div';
  return linkComponent(url);
};

const cardAttrs = (item) => {
  const url = getItemUrl(item);
  if (!url) return {};
  return linkAttrs(url);
};

const safeHtml = (html) => window.sanitizeCmsHtml?.(html) || '';
</script>

<style scoped>
.no-scrollbar::-webkit-scrollbar {
  display: none;
}
.no-scrollbar {
  -ms-overflow-style: none;
  scrollbar-width: none;
}

.content-copy :deep(p) {
  margin: 0 0 0.75rem;
}
.content-copy :deep(p:last-child) {
  margin-bottom: 0;
}
.content-copy :deep(a) {
  color: #ea580c;
  font-weight: 800;
  text-decoration: underline;
}
</style>
