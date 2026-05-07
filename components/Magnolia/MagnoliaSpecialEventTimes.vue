<template>
  <div class="space-y-4">
    <h3 v-if="headingText" class="text-xl font-bold">{{ headingText }}</h3>
    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
      <!-- Special event times would be parsed and listed here -->
      <div v-for="(time, idx) in parsedTimes" :key="idx" class="p-4 bg-white/5 rounded-2xl border border-white/10 flex flex-col gap-1">
        <span class="font-bold text-orange-500">{{ time.day }}</span>
        <span class="text-white">{{ time.time }}</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue';
const props = defineProps({
  headingText: String,
  times: Object // Depending on how Magnolia sends the items map
});

const parsedTimes = computed(() => {
  if (!props.times) return [];
  // Assuming keys like "0", "1" exist
  return Object.keys(props.times)
    .filter(k => /^\d+$/.test(k))
    .sort()
    .map(key => ({
      day: props.times[key].day || 'Sunday',
      time: props.times[key].time || '9:00am, 10:30am, 12:00pm'
    }));
});
</script>
