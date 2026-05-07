<template>
  <section class="relative py-40 overflow-hidden bg-white">
    <!-- Subtle Modern Background Decorative Element -->
    <div class="absolute top-0 left-1/4 w-px h-full bg-gradient-to-b from-transparent via-gray-100 to-transparent"></div>

    <div class="max-w-7xl mx-auto px-8 sm:px-10 lg:px-12 relative z-10">
      <div class="space-y-20">

        <!-- Section Header: Editorial Style -->
        <div class="flex flex-col md:flex-row md:items-end justify-between gap-8">
          <div class="space-y-6">
            <div class="flex items-center gap-4 opacity-50">
              <div class="w-12 h-px bg-gray-900"></div>
              <span class="text-[10px] font-black uppercase tracking-[0.4em] text-gray-900">Your Journey</span>
            </div>
            <h2 class="text-6xl md:text-8xl font-black text-gray-900 tracking-[-0.05em] leading-[0.8]">
              Take your <br/>
              <span class="text-orange-600 italic">next step.</span>
            </h2>
          </div>
          <p class="text-xl text-gray-400 font-light max-w-sm leading-relaxed">
            Growth is a continuous journey. Whether you're new or have been here for years, there's always a way to move forward.
          </p>
        </div>

        <!-- Immersive Card Grid -->
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
          <component
            :is="isExternalUrl(step.url) ? 'a' : 'router-link'"
            v-for="step in steps"
            :key="step.title"
            v-bind="getStepLinkAttrs(step.url)"
            class="group relative aspect-[3/4] rounded-[40px] overflow-hidden shadow-2xl transition-all duration-700 hover:translate-y-[-12px]">

            <!-- Background Image with Zoom & Move -->
            <img :src="step.image" :alt="step.title" class="absolute inset-0 w-full h-full object-cover transform scale-110 group-hover:scale-125 group-hover:rotate-2 transition-transform duration-[2s] ease-out" />

            <!-- Neon Accent Border -->
            <div class="absolute inset-0 border-[3px] border-orange-600/0 rounded-[40px] group-hover:border-orange-600/40 transition-all duration-1000"></div>

            <!-- Gradient Overlay -->
            <div class="absolute inset-0 bg-gradient-to-t from-gray-950 via-gray-950/20 to-transparent group-hover:from-orange-950 transition-colors duration-700"></div>

            <!-- Content Area -->
            <div class="absolute inset-0 p-10 flex flex-col justify-end space-y-4">
              <div class="w-12 h-1 bg-white/30 group-hover:w-full group-hover:bg-orange-500 transition-all duration-700"></div>
              <h3 class="text-3xl font-black text-white tracking-tight uppercase leading-none">
                {{ step.title }}
              </h3>
              <p class="text-sm text-white/60 font-medium tracking-wide translate-y-4 opacity-0 group-hover:translate-y-0 group-hover:opacity-100 transition-all duration-500">
                {{ step.description }}
              </p>
            </div>
          </component>
        </div>

        <!-- Footer Extension -->
        <div class="pt-10 flex justify-center">
          <router-link to="/tools" class="flex flex-col items-center gap-4 group">
            <span class="text-[10px] font-black uppercase tracking-[0.6em] text-gray-300 group-hover:text-orange-600 transition-colors">See all ministry tools</span>
            <div class="w-10 h-10 border border-gray-100 rounded-full flex items-center justify-center text-gray-400 group-hover:bg-orange-600 group-hover:text-white group-hover:border-orange-600 transition-all duration-500">
              <i class="fa-solid fa-plus"></i>
            </div>
          </router-link>
        </div>

      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'NextStepsSection',
  data() {
    return {
      steps: [
        {
          title: 'Ask for Prayer',
          description: 'Share your request and let our community stand with you.',
          image: 'https://cms-images.life.church/lc-site/pages/nextsteps/Prayer.jpg',
          url: 'https://my.life.church/forms/prayer?utm_source=life_church&utm_medium=content_card&utm_campaign=none-ad_no-dept_engagement'
        },
        {
          title: 'Join a LifeGroup',
          description: 'Find a place to belong with people who grow, laugh, and pray together.',
          image: 'https://cms-images.life.church/lc-site/pages/nextsteps/LifeGroups.jpg',
          url: '/lifegroups'
        },
        {
          title: 'Find More Steps',
          description: 'Explore all the ways you can grow your faith and serve others.',
          image: 'https://cms-images.life.church/lc-site/pages/nextsteps/MoreNextSteps.jpg',
          url: '/tools'
        }
      ]
    }
  },
  methods: {
    isExternalUrl(url) {
      return /^https?:\/\//.test(url)
    },
    getStepLinkAttrs(url) {
      if (this.isExternalUrl(url)) {
        return {
          href: url,
          target: '_blank',
          rel: 'noopener noreferrer'
        }
      }

      return {
        to: url
      }
    }
  }
}
</script>
