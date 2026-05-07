<template>
  <section class="py-24 bg-white overflow-hidden">
    <div class="max-w-7xl mx-auto px-8 sm:px-10 lg:px-12">
      <!-- Section Header -->
      <div class="flex flex-col md:flex-row md:items-end justify-between mb-16 gap-8">
        <div class="space-y-4">
          <p class="text-orange-600 font-black uppercase tracking-[0.4em] text-[10px]">Explore Media</p>
          <h2 class="text-4xl md:text-5xl font-black text-gray-900 tracking-tight">Featured Content</h2>
        </div>
        <a href="https://www.life.church/media/" class="group flex items-center gap-3 text-[11px] font-black uppercase tracking-[0.2em] text-gray-400 hover:text-orange-600 transition-colors">
          View All Media
          <div class="w-8 h-8 rounded-full border border-gray-200 flex items-center justify-center group-hover:border-orange-600 group-hover:bg-orange-600 group-hover:text-white transition-all">
            <i class="fa-solid fa-arrow-right"></i>
          </div>
        </a>
      </div>

      <!-- Featured Grid -->
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 mb-20">
        <div v-for="item in media.featured" :key="item.title"
             class="group relative h-[400px] rounded-[2rem] overflow-hidden shadow-2xl transition-all duration-700 hover:scale-[1.02]">
          <img :src="item.image" :alt="item.title" class="absolute inset-0 w-full h-full object-cover transition-transform duration-1000 group-hover:scale-110">
          <div class="absolute inset-0 bg-gradient-to-t from-black via-black/20 to-transparent"></div>

          <div class="absolute inset-0 p-10 flex flex-col justify-end items-start space-y-4">
            <span class="px-4 py-1.5 bg-orange-600 text-white text-[10px] font-black uppercase tracking-[0.2em] rounded-full shadow-lg">New Series</span>
            <h3 class="text-3xl md:text-4xl font-black text-white leading-tight">{{ item.title }}</h3>
            <p class="text-white/70 text-sm max-w-sm font-medium line-clamp-2">{{ item.subTitle }}</p>
            <component
              :is="linkComponent(item.url)"
              v-bind="linkProps(item.url)"
              class="mt-4 px-8 py-3 bg-white text-gray-900 rounded-full text-[11px] font-black uppercase tracking-[0.2em] hover:bg-orange-600 hover:text-white transition-all shadow-xl"
            >
              Watch Now
            </component>
          </div>
        </div>
      </div>

      <!-- Secondary Categories -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-12">
        <!-- Worship -->
        <div class="space-y-8">
          <h4 class="text-[10px] font-black uppercase tracking-[0.4em] text-gray-400">Worship Music</h4>
          <div class="space-y-6">
            <component
              :is="linkComponent(album.url)"
              v-for="album in media.worship"
              :key="album.title"
              v-bind="linkProps(album.url)"
              class="flex items-center gap-4 group/album"
            >
              <div class="w-20 h-20 rounded-2xl overflow-hidden shadow-lg group-hover/album:scale-105 transition-transform duration-500">
                <img :src="album.image" :alt="album.title" class="w-full h-full object-cover">
              </div>
              <div>
                <p class="text-gray-900 font-black text-lg group-hover/album:text-orange-600 transition-colors">{{ album.title }}</p>
                <p class="text-gray-400 text-[10px] font-bold uppercase tracking-widest mt-1">Life.Church Worship</p>
              </div>
            </component>
          </div>
        </div>

        <!-- Stories -->
        <div class="space-y-8">
          <h4 class="text-[10px] font-black uppercase tracking-[0.4em] text-gray-400">Life Stories</h4>
          <div class="space-y-6">
            <component
              :is="linkComponent(story.url)"
              v-for="story in media.stories"
              :key="story.title"
              v-bind="linkProps(story.url)"
              class="group/story block space-y-4"
            >
              <div class="aspect-video rounded-3xl overflow-hidden shadow-lg relative">
                <img :src="story.image" :alt="story.title" class="w-full h-full object-cover group-hover/story:scale-110 transition-transform duration-700">
                <div class="absolute inset-0 bg-black/20 group-hover/story:bg-transparent transition-colors"></div>
                <div class="absolute inset-0 flex items-center justify-center opacity-0 group-hover/story:opacity-100 transition-opacity">
                  <div class="w-12 h-12 bg-white rounded-full flex items-center justify-center shadow-2xl">
                    <i class="fa-solid fa-play text-orange-600 text-sm ml-1"></i>
                  </div>
                </div>
              </div>
              <div>
                <p class="text-gray-900 font-black text-lg leading-tight group-hover/story:text-orange-600 transition-colors">{{ story.title }}</p>
                <p class="text-gray-400 text-[10px] font-bold uppercase tracking-widest mt-1">{{ story.subTitle }}</p>
              </div>
            </component>
          </div>
        </div>

        <!-- Podcast -->
        <div class="space-y-8">
          <h4 class="text-[10px] font-black uppercase tracking-[0.4em] text-gray-400">Leadership Podcast</h4>
          <div v-for="ep in media.podcast" :key="ep.title" class="bg-gray-50 rounded-[2rem] p-8 border border-gray-100 group/pod">
            <div class="w-full aspect-square rounded-2xl overflow-hidden shadow-xl mb-6">
              <img :src="ep.image" :alt="ep.title" class="w-full h-full object-cover group-hover/pod:scale-105 transition-transform duration-700">
            </div>
            <p class="text-orange-600 font-extrabold text-[10px] uppercase tracking-widest mb-2">{{ ep.subTitle }}</p>
            <h5 class="text-xl font-black text-gray-900 leading-snug group-hover/pod:text-orange-600 transition-colors mb-4">{{ ep.title }}</h5>
            <component
              :is="linkComponent(ep.url)"
              v-bind="linkProps(ep.url)"
              class="inline-flex items-center gap-2 text-xs font-black uppercase tracking-widest text-gray-900 border-b-2 border-orange-500 pb-1 hover:text-orange-600 transition-colors"
            >
              Listen Now <i class="fa-solid fa-chevron-right text-[8px]"></i>
            </component>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'MediaSection',
  data() {
    return {
      media: window.siteData.media
    }
  },
  methods: {
    isExternalUrl(url) {
      return /^(https?:)?\/\//.test(url) || /^(mailto|tel):/.test(url)
    },
    linkComponent(url) {
      return this.isExternalUrl(url) ? 'a' : 'router-link'
    },
    linkProps(url) {
      return this.isExternalUrl(url) ? { href: url } : { to: url }
    }
  }
}
</script>
