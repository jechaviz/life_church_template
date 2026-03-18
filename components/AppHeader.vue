<template>
  <header 
    :class="[
      'fixed w-full z-50 transition-all duration-500',
      isScrolled ? 'top-0 glass py-3 shadow-md' : 'top-0 sm:top-[57px] bg-transparent py-5'
    ]"
  >
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex justify-between items-center">
      <!-- Logo -->
      <a href="https://www.life.church/" class="flex items-center gap-2 group">
        <div class="bg-orange-600 p-2 rounded-lg transform group-hover:rotate-12 transition-transform duration-300">
          <i class="fa-solid fa-shapes text-white text-2xl"></i>
        </div>
        <span :class="['font-black text-2xl tracking-tighter transition-colors duration-300', isScrolled ? 'text-gray-900' : 'text-white']">
          LIFE.CHURCH
        </span>
      </a>

      <!-- Desktop Nav -->
      <nav class="hidden lg:flex items-center gap-8">
        <a v-for="link in mainLinks" :key="link.name" :href="link.url"
           :class="['text-[13px] uppercase tracking-widest font-bold hover:text-orange-500 transition-colors relative group/link', isScrolled ? 'text-gray-700' : 'text-white']">
          {{ link.name }}
          <span class="absolute -bottom-1 left-0 w-0 h-0.5 bg-orange-500 transition-all duration-300 group-hover/link:w-full"></span>
        </a>
        
        <!-- Ways to Connect Dropdown -->
        <div class="relative group">
          <button :class="['text-[13px] uppercase tracking-widest font-bold hover:text-orange-500 transition-colors flex items-center gap-1', isScrolled ? 'text-gray-700' : 'text-white']">
            Connect <i class="fa-solid fa-chevron-down text-[10px] opacity-70 group-hover:rotate-180 transition-transform"></i>
          </button>
          <div class="absolute left-1/2 -translate-x-1/2 mt-4 w-64 bg-white rounded-2xl shadow-2xl opacity-0 invisible group-hover:opacity-100 group-hover:visible transition-all duration-300 transform origin-top scale-95 group-hover:scale-100 overflow-hidden border border-gray-100 p-2">
            <div class="grid grid-cols-1 gap-1">
              <a v-for="sub in connectLinks" :key="sub.name" :href="sub.url" class="flex items-center gap-3 px-4 py-3 text-sm font-semibold text-gray-700 hover:bg-orange-50 hover:text-orange-600 rounded-xl transition-all duration-200">
                <i class="fa-solid fa-circle text-[4px] opacity-30"></i>
                {{ sub.name }}
              </a>
            </div>
          </div>
        </div>

        <!-- About Us Dropdown -->
        <div class="relative group">
          <button :class="['text-[13px] uppercase tracking-widest font-bold hover:text-orange-500 transition-colors flex items-center gap-1', isScrolled ? 'text-gray-700' : 'text-white']">
            About <i class="fa-solid fa-chevron-down text-[10px] opacity-70 group-hover:rotate-180 transition-transform"></i>
          </button>
          <div class="absolute left-1/2 -translate-x-1/2 mt-4 w-64 bg-white rounded-2xl shadow-2xl opacity-0 invisible group-hover:opacity-100 group-hover:visible transition-all duration-300 transform origin-top scale-95 group-hover:scale-100 overflow-hidden border border-gray-100 p-2">
            <div class="grid grid-cols-1 gap-1">
              <a v-for="sub in aboutLinks" :key="sub.name" :href="sub.url" class="flex items-center gap-3 px-4 py-3 text-sm font-semibold text-gray-700 hover:bg-orange-50 hover:text-orange-600 rounded-xl transition-all duration-200">
                <i class="fa-solid fa-circle text-[4px] opacity-30"></i>
                {{ sub.name }}
              </a>
            </div>
          </div>
        </div>
      </nav>

      <!-- Desktop Actions -->
      <div class="hidden lg:flex items-center gap-6">
        <a href="https://my.life.church/login" :class="['text-xs font-black uppercase tracking-widest hover:text-orange-500 transition-all flex items-center gap-2', isScrolled ? 'text-gray-700' : 'text-white']">
          <i class="fa-solid fa-circle-user text-lg"></i> Sign In
        </a>
      </div>

      <!-- Mobile menu button -->
      <button @click="isMobileMenuOpen = !isMobileMenuOpen" class="lg:hidden w-10 h-10 flex items-center justify-center rounded-full transition-colors" :class="isScrolled || isMobileMenuOpen ? 'bg-gray-100 text-gray-800' : 'bg-white/10 text-white'">
        <i :class="isMobileMenuOpen ? 'fa-solid fa-xmark' : 'fa-solid fa-bars'"></i>
      </button>
    </div>

    <!-- Mobile Nav Overlay -->
    <transition
      enter-active-class="transition duration-300 ease-out"
      enter-from-class="opacity-0 translate-y-4"
      enter-to-class="opacity-100 translate-y-0"
      leave-active-class="transition duration-200 ease-in"
      leave-from-class="opacity-100 translate-y-0"
      leave-to-class="opacity-0 translate-y-4"
    >
      <div v-show="isMobileMenuOpen" class="lg:hidden absolute top-full left-0 w-full bg-white shadow-2xl border-t border-gray-100 flex flex-col h-[calc(100vh-80px)] overflow-hidden">
        <div class="flex-grow px-6 py-8 flex flex-col gap-2 overflow-y-auto">
          <a v-for="link in mainLinks" :key="link.name" :href="link.url" class="block py-4 text-gray-900 text-xl font-black border-b border-gray-50 uppercase tracking-tighter">
            {{ link.name }}
          </a>
          
          <div class="py-6 border-b border-gray-50">
            <div class="font-black text-gray-400 uppercase text-[10px] tracking-widest mb-4">Ways to Connect</div>
            <div class="grid grid-cols-2 gap-x-4 gap-y-2">
              <a v-for="sub in connectLinks" :key="sub.name" :href="sub.url" class="block py-2 text-gray-700 text-sm font-bold">
                {{ sub.name }}
              </a>
            </div>
          </div>

          <div class="py-6">
            <div class="font-black text-gray-400 uppercase text-[10px] tracking-widest mb-4">About Us</div>
            <div class="grid grid-cols-2 gap-x-4 gap-y-2">
              <a v-for="sub in aboutLinks" :key="sub.name" :href="sub.url" class="block py-2 text-gray-700 text-sm font-bold">
                {{ sub.name }}
              </a>
            </div>
          </div>
        </div>
        
        <div class="p-6 bg-gray-50 mt-auto">
          <a href="https://my.life.church/login" class="block py-4 text-center text-white font-black bg-orange-600 rounded-2xl shadow-lg shadow-orange-600/30 uppercase tracking-widest">
            <i class="fa-solid fa-circle-user mr-2"></i> Sign In
          </a>
        </div>
      </div>
    </transition>
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
      // Adjusted threshold for TopBanner (around 57px)
      this.isScrolled = window.scrollY > 40
    }
  }
}
</script>
