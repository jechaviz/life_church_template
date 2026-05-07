<template>
  <div class="w-full max-w-4xl mx-auto space-y-4">
    <div v-if="items">
      <div v-for="(subItem, idx) in sortedItems" :key="idx" class="magnolia-accordion-item-wrapper">
        <MagnoliaZone :area="{ '0': subItem }" area-name="accordion-item" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  singleSelect: Boolean,
  sbOnMobile: String,
  sbOnTabletAndUp: String,
  items: Object
});

const sortedItems = computed(() => {
  if (!props.items) return [];
  return Object.keys(props.items)
    .filter(key => /^\d+$/.test(key))
    .sort((a, b) => parseInt(a) - parseInt(b))
    .map(key => props.items[key]);
});
</script>
