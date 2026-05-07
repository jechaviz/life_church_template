<template>
  <section
    class="magnolia-dual-content-zone relative overflow-hidden"
    :class="[bgcolor, pyOnMobile, pyOnTabletAndUp, sbOnMobile, sbOnTabletAndUp]"
  >
    <!-- Background Image -->
    <div
      v-if="backgroundImage_public"
      class="absolute inset-0 w-full h-full bg-cover bg-center -z-10"
      :style="{ backgroundImage: `url(${backgroundImage_public})` }"
    ></div>

    <div class="container mx-auto px-6 grid grid-cols-1 md:grid-cols-2 gap-12 items-center relative z-10">
      <div
        class="area-left h-full flex flex-col justify-center"
        :class="[alignTabletMobile]"
      >
        <MagnoliaZone v-if="arealeft" :area="arealeft" area-name="arealeft" :color-theme="colorTheme" />
      </div>
      <div
        class="area-right h-full flex flex-col justify-center"
      >
        <MagnoliaZone v-if="arearight" :area="arearight" area-name="arearight" :color-theme="colorTheme" />
      </div>
    </div>
  </section>
</template>

<script setup>
const props = defineProps({
  bgcolor: {
    type: String,
    default: 'transparent'
  },
  backgroundImage_public: String,
  pyOnMobile: String,
  pyOnTabletAndUp: String,
  sbOnMobile: String,
  sbOnTabletAndUp: String,
  alignTabletMobile: String,
  colorTheme: String,
  arealeft: Object,
  arearight: Object
});
</script>
