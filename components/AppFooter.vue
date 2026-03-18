<template>
  <footer class="bg-gray-900 text-white pt-20 pb-10 border-t-4 border-orange-500">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      
      <!-- Top Section: Links & Social -->
      <div class="flex flex-col md:flex-row justify-between items-center md:items-start gap-12 mb-16">
        
        <!-- Left: Logo & Links -->
        <div class="w-full md:w-2/3 flex flex-col md:flex-row items-center md:items-start gap-10">
          <div class="flex-shrink-0 mb-6 md:mb-0">
            <a href="/" class="flex items-center gap-2 group">
              <div class="bg-gray-800 p-3 rounded-xl group-hover:bg-orange-500 transition-colors duration-300">
                <i class="fa-solid fa-shapes text-orange-500 group-hover:text-white text-3xl transition-colors duration-300"></i>
              </div>
            </a>
          </div>
          
          <div class="w-full grid grid-cols-2 sm:grid-cols-4 gap-6 text-center md:text-left">
            <div v-for="(col, i) in linkColumns" :key="i" class="flex flex-col gap-3">
              <a v-for="link in col" :key="link.name" :href="link.url" class="text-sm text-gray-400 hover:text-white transition-colors duration-200">
                {{ link.name }}
              </a>
            </div>
          </div>
        </div>

        <!-- Right: Social -->
        <div class="w-full md:w-1/3 flex flex-col items-center md:items-end gap-6">
          <h4 class="text-sm font-bold tracking-widest text-gray-500 uppercase">Connect</h4>
          <div class="flex gap-4">
            <a v-for="social in socials" :key="social.name" :href="social.url" :aria-label="social.name" target="_blank" class="w-10 h-10 rounded-full bg-gray-800 flex items-center justify-center text-gray-400 hover:bg-orange-600 hover:text-white transform hover:-translate-y-1 transition-all duration-300">
              <i :class="social.icon" class="text-lg"></i>
            </a>
          </div>
        </div>

      </div>

      <!-- Bottom Section: Legal -->
      <div class="border-t border-gray-800 pt-8 flex flex-col items-center text-center space-y-4">
        <p class="text-gray-400 text-sm">
          Attend <a href="https://live.life.church" class="text-orange-500 hover:underline">Life.Church Online</a> or a <a href="https://www.life.church/locations" class="text-orange-500 hover:underline">Life.Church location</a>.
        </p>
        <div class="flex flex-wrap justify-center gap-4 text-xs text-gray-500">
          <a href="#" class="hover:text-white transition-colors">Privacy Policy</a>
          <span>|</span>
          <a href="#" class="hover:text-white transition-colors">Terms of Use</a>
          <span>|</span>
          <a href="#" class="hover:text-white transition-colors">Vulnerability Disclosure Program</a>
        </div>
        <p class="text-xs text-gray-600 mt-4">
          &copy; {{ new Date().getFullYear() }} Life.Church. All rights reserved.
        </p>
      </div>

    </div>
  </footer>
</template>

<script>
export default {
  name: 'AppFooter',
  data() {
    return {
      linkColumns: [
        [ { name: 'Watch', url: '#' }, { name: 'Locations', url: '#' } ],
        [ { name: 'Give', url: '#' }, { name: 'Tools', url: '#' } ],
        [ { name: 'For Churches', url: '#' }, { name: 'Careers', url: '#' } ],
        [ { name: 'Shop', url: '#' }, { name: 'Contact Us', url: '#' } ]
      ],
      socials: [
        { name: 'Facebook', icon: 'fa-brands fa-facebook-f', url: '#' },
        { name: 'Instagram', icon: 'fa-brands fa-instagram', url: '#' },
        { name: 'TikTok', icon: 'fa-brands fa-tiktok', url: '#' },
        { name: 'YouTube', icon: 'fa-brands fa-youtube', url: '#' },
        { name: 'LinkedIn', icon: 'fa-brands fa-linkedin-in', url: '#' }
      ]
    }
  }
}
</script>
