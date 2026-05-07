<template>
  <div class="magnolia-zone" :class="areaName">
    <template v-for="(item, index) in sortedComponents" :key="item['@id'] || index">
      <component
        :is="getComponentType(item['mgnl:template'])"
        v-if="getComponentType(item['mgnl:template'])"
        v-bind="item"
        :color-theme="colorTheme"
      />
      <div v-else-if="debug" class="debug-unknown-component p-4 border border-dashed border-red-500 m-2">
        Unknown template: {{ item['mgnl:template'] }}
      </div>
    </template>
  </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  area: {
    type: Object,
    required: true
  },
  areaName: String,
  colorTheme: String,
  isArea: {
    type: String,
    default: 'main'
  },
  debug: {
    type: Boolean,
    default: false
  }
});

/**
 * Components in Magnolia are often stored as an object with numeric keys "0", "1", "2"...
 * We need to sort them numerically to preserve correct page order.
 */
const sortedComponents = computed(() => {
  if (!props.area) return [];
  
  // Filter out meta properties like "@name", "@id", etc.
  return Object.keys(props.area)
    .filter(key => /^\d+$/.test(key))
    .sort((a, b) => parseInt(a) - parseInt(b))
    .map(key => props.area[key]);
});

const getComponentType = (template) => {
  if (!template) return null;
  
  const templateMap = {
    'lifechurch:components/singlecontentzone': 'MagnoliaSingleContentZone',
    'lifechurch:components/dualcontentzone': 'MagnoliaDualContentZone',
    'lifechurch:components/heading': 'MagnoliaHeading',
    'lifechurch:components/spacer': 'MagnoliaSpacer',
    'lifechurch:components/opencontentlist': 'MagnoliaContentList',
    'lifechurch:components/opencontentlistcards': 'MagnoliaContentList',
    'lifechurch:components/richtext': 'MagnoliaRichText',
    'lifechurch:components/compositebuttongroup': 'MagnoliaCompositeButtonGroup',
    'lifechurch:components/locationslisting': 'MagnoliaLocationsListing',
    'lifechurch:components/mediacollectionlisting': 'MagnoliaMediaCollectionListing',
    'lifechurch:components/mediaasset': 'MagnoliaMediaAsset',
    'lifechurch:components/accordion': 'MagnoliaAccordion',
    'lifechurch:components/accordionitem': 'MagnoliaAccordionItem',
    'lifechurch:components/video': 'MagnoliaVideo',
    'lifechurch:components/embeditem': 'MagnoliaEmbedItem',
    'lifechurch:components/banner': 'MagnoliaBanner',
    'lifechurch:components/copythistext': 'MagnoliaCopyThisText',
    'lifechurch:components/specialeventtimes': 'MagnoliaSpecialEventTimes'
  };
  
  return templateMap[template] || null;
};
</script>
