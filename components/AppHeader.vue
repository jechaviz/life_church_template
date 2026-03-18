<template>
  <header :class="['fixed w-full top-0 z-50 transition-all duration-300', isScrolled || isMobileMenuOpen ? 'glass py-3 shadow-sm' : 'bg-transparent py-5']">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex justify-between items-center">
      <!-- Logo -->
      <a href="/" class="flex items-center gap-2">
        <!-- Using a placeholder icon since I don't have the Life.Church SVG -->
        <i class="fa-solid fa-shapes text-orange-500 text-3xl"></i>
        <span :class="['font-bold text-2xl tracking-tight transition-colors duration-300', isScrolled || isMobileMenuOpen ? 'text-gray-900' : 'text-white']">
          Life.Church
        </span>
      </a>

      <!-- Desktop Nav -->
      <nav class="hidden lg:flex items-center gap-6">
        <a v-for="link in mainLinks" :key="link.name" :href="link.url"
           :class="['text-sm font-semibold hover:text-orange-500 transition-colors', isScrolled ? 'text-gray-700' : 'text-white']">
          {{ link.name }}
        </a>
        
        <!-- Ways to Connect Dropdown -->
        <div class="relative group">
          <button :class="['text-sm font-semibold hover:text-orange-500 transition-colors flex items-center gap-1', isScrolled ? 'text-gray-700' : 'text-white']">
            Ways to Connect <i class="fa-solid fa-chevron-down text-[10px] opacity-70"></i>
          </button>
          <div class="absolute left-0 mt-2 w-56 bg-white rounded-xl shadow-xl opacity-0 invisible group-hover:opacity-100 group-hover:visible transition-all duration-300 transform origin-top-left scale-95 group-hover:scale-100 overflow-hidden border border-gray-100">
            <a v-for="sub in connectLinks" :key="sub.name" :href="sub.url" class="block px-4 py-3 text-sm text-gray-700 hover:bg-orange-50 hover:text-orange-600 transition-colors">
              {{ sub.name }}
            </a>
          </div>
        </div>

        <!-- About Us Dropdown -->
        <div class="relative group">
          <button :class="['text-sm font-semibold hover:text-orange-500 transition-colors flex items-center gap-1', isScrolled ? 'text-gray-700' : 'text-white']">
            About Us <i class="fa-solid fa-chevron-down text-[10px] opacity-70"></i>
          </button>
          <div class="absolute left-0 mt-2 w-56 bg-white rounded-xl shadow-xl opacity-0 invisible group-hover:opacity-100 group-hover:visible transition-all duration-300 transform origin-top-left scale-95 group-hover:scale-100 overflow-hidden border border-gray-100">
            <a v-for="sub in aboutLinks" :key="sub.name" :href="sub.url" class="block px-4 py-3 text-sm text-gray-700 hover:bg-orange-50 hover:text-orange-600 transition-colors">
              {{ sub.name }}
            </a>
          </div>
        </div>
      </nav>

      <!-- Desktop Actions -->
      <div class="hidden lg:flex items-center gap-4">
        <a href="#" :class="['text-sm font-semibold hover:text-orange-500 transition-all flex items-center gap-2', isScrolled ? 'text-gray-700' : 'text-white']">
          <i class="fa-solid fa-user text-sm"></i> Sign In
        </a>
      </div>

      <!-- Mobile menu button -->
      <button @click="isMobileMenuOpen = !isMobileMenuOpen" class="lg:hidden text-2xl transition-colors" :class="isScrolled || isMobileMenuOpen ? 'text-gray-800 hover:text-orange-500' : 'text-white hover:text-orange-200'">
        <i :class="isMobileMenuOpen ? 'fa-solid fa-xmark' : 'fa-solid fa-bars'"></i>
      </button>
    </div>

    <!-- Mobile Nav -->
    <div v-show="isMobileMenuOpen" class="lg:hidden absolute top-full left-0 w-full bg-white shadow-xl border-t border-gray-100 flex flex-col">
      <div class="px-4 py-2 flex flex-col gap-2 overflow-y-auto max-h-[80vh]">
        <a v-for="link in mainLinks" :key="link.name" :href="link.url" class="block py-3 text-gray-800 font-semibold border-b border-gray-50">
          {{ link.name }}
        </a>
        <div class="py-2 border-b border-gray-50">
          <div class="font-bold text-gray-400 uppercase text-xs tracking-wider mb-2">Ways to Connect</div>
          <a v-for="sub in connectLinks" :key="sub.name" :href="sub.url" class="block py-2 pl-4 text-gray-700 text-sm">
            {{ sub.name }}
          </a>
        </div>
        <div class="py-2 border-b border-gray-50">
          <div class="font-bold text-gray-400 uppercase text-xs tracking-wider mb-2">About Us</div>
          <a v-for="sub in aboutLinks" :key="sub.name" :href="sub.url" class="block py-2 pl-4 text-gray-700 text-sm">
            {{ sub.name }}
          </a>
        </div>
        <a href="#" class="block py-4 text-center text-orange-600 font-bold bg-orange-50 rounded-xl mt-2 mb-4">
          <i class="fa-solid fa-user mr-2"></i> Sign In
        </a>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: 'AppHeader',
  data() {
    return {
      isScrolled: false,
      isMobileMenuOpen: false,
      mainLinks: [
        { name: 'Media', url: 'https://www.life.church/media/' },
        { name: 'Locations', url: 'https://www.life.church/locations/' },
        { name: 'Give', url: 'https://www.life.church/giving/' },
        { name: 'Who We Are', url: 'https://www.life.church/who-we-are/' },
        { name: 'Worship', url: 'https://www.life.church/worship/' }
      ],
      connectLinks: [
        { name: 'Kids', url: 'https://www.life.church/kids/' },
        { name: 'Youth', url: 'https://www.life.church/switch/' },
        { name: 'LifeGroups', url: 'https://www.life.church/lifegroups/' },
        { name: 'Missions', url: 'https://www.life.church/missions/' },
        { name: 'You Said Yes', url: 'https://www.life.church/yes/' },
        { name: 'Start Serving', url: 'https://www.life.church/serving/' },
        { name: 'Grow Your Faith', url: 'https://www.life.church/tools/' },
        { name: 'Careers', url: 'https://www.life.church/careers/' },
        { name: 'Store', url: 'https://shop.life.church/' }
      ],
      aboutLinks: [
        { name: 'Our Beliefs', url: 'https://www.life.church/who-we-are/our-beliefs/' },
        { name: 'What to Expect', url: 'https://www.life.church/who-we-are/what-to-expect/' },
        { name: 'For Churches', url: 'https://www.life.church/churches/' },
        { name: 'Contact Us', url: 'https://www.life.church/contact/' }
      ]
    }
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll, { passive: true })
    this.handleScroll()
  },
  unmounted() {
    window.removeEventListener('scroll', this.handleScroll)
  },
  methods: {
    handleScroll() {
      this.isScrolled = window.scrollY > 20
    }
  }
}
</script>
