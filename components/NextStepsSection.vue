<template>
  <section class="py-20 bg-gray-50 border-t border-gray-100">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      
      <!-- Section Header -->
      <div class="text-center mb-16">
        <h2 class="text-3xl md:text-5xl font-extrabold text-gray-900 tracking-tight">
          Take Your Next Step
        </h2>
        <div class="w-24 h-1 bg-orange-500 mx-auto mt-6 rounded-full"></div>
      </div>

      <!-- Cards Grid -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
        <a v-for="(card, index) in steps" :key="index" :href="card.url" class="group relative block h-96 rounded-2xl overflow-hidden shadow-lg hover:shadow-2xl transition-all duration-500 hover:-translate-y-2">
          
          <!-- Background Image with Zoom on Hover -->
          <div class="absolute inset-0 w-full h-full">
            <img :src="card.image" :alt="card.title" class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110" />
            <div class="absolute inset-0 bg-gradient-to-t from-gray-900 via-gray-900/40 to-transparent opacity-80 group-hover:opacity-90 transition-opacity duration-300"></div>
          </div>

          <!-- Card Content -->
          <div class="absolute inset-0 p-8 flex flex-col justify-end text-white z-10">
            <div class="transform transition-transform duration-300 group-hover:-translate-y-4">
              <h3 class="text-2xl font-bold mb-2">{{ card.title }}</h3>
              <p class="text-gray-200 font-light line-clamp-2">{{ card.description }}</p>
            </div>
            
            <!-- Hover Action Area -->
            <div class="absolute bottom-6 left-8 right-8 opacity-0 group-hover:opacity-100 transition-all duration-300 transform translate-y-4 group-hover:translate-y-0 flex items-center gap-2 text-orange-400 font-semibold">
              <span>View Details</span>
              <i class="fa-solid fa-arrow-right text-sm"></i>
            </div>
          </div>
        </a>
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
          description: "We'd love to pray with you.",
          image: 'https://cms-images.life.church/lc-site/pages/nextsteps/Prayer.jpg',
          url: 'https://my.life.church/forms/prayer'
        },
        {
          title: 'Join a LifeGroup',
          description: "Find the people you can grow, laugh, and pray with.",
          image: 'https://cms-images.life.church/lc-site/pages/nextsteps/LifeGroups.jpg',
          url: 'https://life.church/lifegroups/search'
        },
        {
          title: 'Find More Next Steps',
          description: "Discover the next step on your journey.",
          image: 'https://cms-images.life.church/lc-site/pages/nextsteps/MoreNextSteps.jpg',
          url: 'https://www.life.church/nextsteps'
        }
      ]
    }
  }
}
</script>
