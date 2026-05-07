<template>
  <header
    @keydown.escape="closeMenus"
    :class="[
      'fixed w-full z-100 transition-all duration-700 ease-in-out',
      isScrolled ? 'top-0 glass-premium py-2 shadow-2xl' : 'top-0 sm:top-[57px] bg-transparent py-4'
    ]"
  >
    <div class="max-w-7xl mx-auto px-6 sm:px-8 lg:px-10 flex justify-between items-center">
      <!-- Logo Area -->
      <router-link to="/" class="flex items-center gap-3 group">
        <div class="relative w-10 h-10 flex items-center justify-center">
          <div class="absolute inset-0 bg-orange-600 rounded-xl transform group-hover:rotate-6 transition-transform duration-500 shadow-lg shadow-orange-600/20"></div>
          <i class="fa-solid fa-shapes text-white text-xl relative z-10"></i>
        </div>
        <div class="flex flex-col -space-y-1">
          <span :class="['font-black text-xl tracking-[-0.05em] transition-colors duration-500', isScrolled ? 'text-gray-900' : 'text-white']">
            LIFE.CHURCH
          </span>
          <span :class="['text-[8px] uppercase tracking-[0.3em] font-bold opacity-50', isScrolled ? 'text-gray-500' : 'text-gray-300']">
            ESTABLISHED 1996
          </span>
        </div>
      </router-link>

      <!-- Desktop Navigation -->
      <nav class="hidden lg:flex items-center gap-10">
        <router-link v-for="link in navigation.main" :key="link.name" :to="link.url"
           :class="['text-[11px] uppercase tracking-[0.2em] font-extrabold hover:text-orange-500 transition-all relative group/link text-nowrap', isScrolled ? 'text-gray-600' : 'text-white/90']">
          {{ link.name }}
          <span class="absolute -bottom-2 left-0 w-0 h-0.5 bg-orange-500 transition-all duration-500 group-hover/link:w-full"></span>
        </router-link>

        <!-- Multi-level Dropdowns (Mega Menu style) -->
        <div class="relative" @mouseenter="openMenu = 'connect'" @mouseleave="closeMenu('connect')">
          <button
            type="button"
            aria-haspopup="true"
            :aria-expanded="isMenuOpen('connect') ? 'true' : 'false'"
            @click.stop="toggleMenu('connect')"
            :class="['appearance-none bg-transparent border-0 p-0 text-[11px] uppercase tracking-[0.2em] font-extrabold hover:text-orange-500 transition-all flex items-center gap-1.5', isScrolled ? 'text-gray-600' : 'text-white/90']"
          >
            Connect <i :class="['fa-solid fa-chevron-down text-[8px] opacity-40 transition-transform duration-300', isMenuOpen('connect') ? 'rotate-180' : '']"></i>
          </button>
          <div :class="[
            'absolute left-1/2 -translate-x-1/2 mt-6 w-[700px] bg-white/95 backdrop-blur-2xl rounded-3xl shadow-[0_30px_60px_-15px_rgba(0,0,0,0.4)] transition-all duration-300 transform origin-top max-h-[85vh] overflow-y-auto border border-white/30 p-8 z-[200]',
            isMenuOpen('connect') ? 'opacity-100 visible scale-100' : 'opacity-0 invisible scale-95'
          ]">
            <div class="grid grid-cols-2 gap-4">
              <template v-for="sub in navigation.connect" :key="sub.name">
                <a
                  v-if="isExternalLink(sub.url)"
                  :href="sub.url"
                  target="_blank"
                  rel="noopener noreferrer"
                  @click="closeMenus"
                  class="flex items-start gap-4 p-4 text-gray-700 hover:bg-orange-600 hover:text-white rounded-2xl transition-all duration-400 group/item"
                >
                  <div class="w-10 h-10 flex items-center justify-center bg-gray-100 rounded-xl group-hover/item:bg-white/20 transition-colors">
                    <i :class="['fa-solid', sub.icon || 'fa-circle-dot', 'text-lg text-orange-600 group-hover/item:text-white']"></i>
                  </div>
                  <div class="flex-grow pt-1">
                    <div class="flex items-center justify-between">
                      <span class="text-[14px] font-black uppercase tracking-wider">{{ sub.name }}</span>
                      <i class="fa-solid fa-arrow-up-right-from-square text-[8px] opacity-0 -translate-x-2 group-hover/item:opacity-50 group-hover/item:translate-x-0 transition-all"></i>
                    </div>
                    <p class="text-[11px] font-medium opacity-60 mt-1 leading-relaxed group-hover/item:opacity-90">{{ sub.excerpt }}</p>
                  </div>
                </a>
                <router-link
                  v-else
                  :to="sub.url"
                  @click="closeMenus"
                  class="flex items-start gap-4 p-4 text-gray-700 hover:bg-orange-600 hover:text-white rounded-2xl transition-all duration-400 group/item"
                >
                  <div class="w-10 h-10 flex items-center justify-center bg-gray-100 rounded-xl group-hover/item:bg-white/20 transition-colors">
                    <i :class="['fa-solid', sub.icon || 'fa-circle-dot', 'text-lg text-orange-600 group-hover/item:text-white']"></i>
                  </div>
                  <div class="flex-grow pt-1">
                    <div class="flex items-center justify-between">
                      <span class="text-[14px] font-black uppercase tracking-wider">{{ sub.name }}</span>
                      <i class="fa-solid fa-arrow-right text-[10px] opacity-0 -translate-x-2 group-hover/item:opacity-50 group-hover/item:translate-x-0 transition-all"></i>
                    </div>
                    <p class="text-[11px] font-medium opacity-60 mt-1 leading-relaxed group-hover/item:opacity-90">{{ sub.excerpt }}</p>
                  </div>
                </router-link>
              </template>
            </div>
          </div>
        </div>

        <div class="relative" @mouseenter="openMenu = 'about'" @mouseleave="closeMenu('about')">
          <button
            type="button"
            aria-haspopup="true"
            :aria-expanded="isMenuOpen('about') ? 'true' : 'false'"
            @click.stop="toggleMenu('about')"
            :class="['appearance-none bg-transparent border-0 p-0 text-[11px] uppercase tracking-[0.2em] font-extrabold hover:text-orange-500 transition-all flex items-center gap-1.5', isScrolled ? 'text-gray-600' : 'text-white/90']"
          >
            About <i :class="['fa-solid fa-chevron-down text-[8px] opacity-40 transition-transform duration-300', isMenuOpen('about') ? 'rotate-180' : '']"></i>
          </button>
          <div :class="[
            'absolute left-1/2 -translate-x-1/2 mt-6 w-80 bg-white/95 backdrop-blur-2xl rounded-3xl shadow-[0_30px_60px_-15px_rgba(0,0,0,0.3)] transition-all duration-300 transform origin-top overflow-hidden border border-white/20 p-3',
            isMenuOpen('about') ? 'opacity-100 visible scale-100' : 'opacity-0 invisible scale-95'
          ]">
            <div class="grid grid-cols-1 gap-1">
              <router-link v-for="sub in navigation.about" :key="sub.name" :to="sub.url" @click="closeMenus" class="flex flex-col px-5 py-4 text-gray-700 hover:bg-slate-900 hover:text-white rounded-2xl transition-all duration-300 group/item">
                <span class="text-[12px] font-black uppercase tracking-widest">{{ sub.name }}</span>
                <span class="text-[10px] opacity-50 group-hover/item:opacity-70 mt-1">{{ sub.excerpt }}</span>
              </router-link>
            </div>
          </div>
        </div>
      </nav>

      <!-- Desktop Actions -->
      <div class="hidden lg:flex items-center gap-8">
        <a href="https://my.life.church/login"
           :class="[
             'px-6 py-2.5 rounded-full text-[11px] font-black uppercase tracking-[0.2em] shadow-lg transition-all duration-500 flex items-center gap-2 group',
             isScrolled
               ? 'bg-orange-600 text-white hover:bg-orange-700 shadow-orange-600/20'
               : 'bg-white/10 text-white hover:bg-white hover:text-orange-600 border border-white/20'
           ]">
          <i class="fa-solid fa-circle-user text-base group-hover:scale-110 transition-transform"></i>
          Sign In
        </a>
      </div>

      <!-- Mobile Menu Button -->
      <button @click="isMobileMenuOpen = !isMobileMenuOpen"
              type="button"
              aria-label="Toggle navigation menu"
              :aria-expanded="isMobileMenuOpen ? 'true' : 'false'"
              class="lg:hidden h-10 px-4 rounded-full flex items-center gap-2 transition-all duration-500 overflow-hidden border"
              :class="isScrolled || isMobileMenuOpen
                ? 'bg-gray-100 border-gray-200 text-gray-900'
                : 'bg-white/10 border-white/20 text-white'"
      >
        <div class="relative w-6 h-6 flex flex-col justify-center items-center gap-1">
          <span :class="['w-5 h-0.5 transition-all duration-300', isMobileMenuOpen ? 'rotate-45 translate-y-1.5' : '', isScrolled || isMobileMenuOpen ? 'bg-gray-900' : 'bg-white']"></span>
          <span :class="['w-5 h-0.5 transition-all duration-300', isMobileMenuOpen ? 'opacity-0' : '', isScrolled || isMobileMenuOpen ? 'bg-gray-900' : 'bg-white']"></span>
          <span :class="['w-5 h-0.5 transition-all duration-300', isMobileMenuOpen ? '-rotate-45 -translate-y-1.5' : '', isScrolled || isMobileMenuOpen ? 'bg-gray-900' : 'bg-white']"></span>
        </div>
      </button>
    </div>

    <!-- Mobile Nav Overlay -->
    <transition
      enter-active-class="transition-all duration-700 ease-[cubic-bezier(0.23,1,0.32,1)]"
      enter-from-class="opacity-0 translate-x-full"
      enter-to-class="opacity-100 translate-x-0"
      leave-active-class="transition-all duration-500 ease-in"
      leave-from-class="opacity-100 translate-x-0"
      leave-to-class="opacity-0 translate-x-full"
    >
      <div v-show="isMobileMenuOpen" class="lg:hidden fixed inset-y-0 right-0 w-[85%] bg-white/98 backdrop-blur-3xl shadow-[-50px_0_100px_rgba(0,0,0,0.1)] flex flex-col z-[110]">
        <div class="flex-grow px-10 py-12 flex flex-col gap-8 overflow-y-auto">
          <div class="space-y-4">
            <p class="text-[10px] font-black text-orange-600 uppercase tracking-[0.4em]">Explore</p>
            <component
              v-for="link in navigation.main"
              :key="link.name"
              :is="getMobileLinkTag(link.url)"
              v-bind="getMobileLinkProps(link.url)"
              @click="closeMobileMenu"
              class="block py-2 text-gray-900 text-3xl font-black"
            >
              {{ link.name }}
            </component>
          </div>
          <div class="space-y-6">
            <p class="text-[10px] font-black text-gray-400 uppercase tracking-[0.4em]">Connect</p>
            <div class="grid grid-cols-1 gap-y-6">
              <component
                v-for="sub in navigation.connect"
                :key="sub.name"
                :is="getMobileLinkTag(sub.url)"
                v-bind="getMobileLinkProps(sub.url)"
                @click="closeMobileMenu"
                class="flex items-center gap-5"
              >
                <div class="w-12 h-12 rounded-2xl bg-gray-100 flex items-center justify-center text-orange-600 shadow-sm">
                  <i :class="['fa-solid', sub.icon || 'fa-circle-dot', 'text-xl']"></i>
                </div>
                <div>
                  <p class="text-gray-900 text-lg font-black leading-tight">{{ sub.name }}</p>
                  <p class="text-gray-500 text-[11px] font-bold mt-0.5 uppercase tracking-wide opacity-70">{{ sub.excerpt }}</p>
                </div>
              </component>
            </div>
          </div>
        </div>
        <div class="p-10 bg-gray-50/50 backdrop-blur-lg mt-auto">
          <a href="https://my.life.church/login" class="block py-5 text-center text-white font-black bg-orange-600 rounded-3xl shadow-2xl shadow-orange-600/30 uppercase tracking-[0.2em]">
            Join My.Life.Church
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
      openMenu: null,
      navigation: window.siteData.navigation
    }
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll, { passive: true })
    document.addEventListener('click', this.handleDocumentClick)
    this.handleScroll()
  },
  unmounted() {
    window.removeEventListener('scroll', this.handleScroll)
    document.removeEventListener('click', this.handleDocumentClick)
  },
  methods: {
    toggleMenu(menu) {
      this.openMenu = this.openMenu === menu ? null : menu
    },
    isMenuOpen(menu) {
      return this.openMenu === menu
    },
    closeMenu(menu) {
      if (this.openMenu === menu) this.openMenu = null
    },
    closeMenus() {
      this.openMenu = null
    },
    closeMobileMenu() {
      this.isMobileMenuOpen = false
    },
    handleDocumentClick(event) {
      if (!this.$el.contains(event.target)) this.closeMenus()
    },
    getMobileLinkTag(url) {
      return this.isExternalLink(url) ? 'a' : 'router-link'
    },
    getMobileLinkProps(url) {
      return this.isExternalLink(url)
        ? {
            href: url,
            target: '_blank',
            rel: 'noopener noreferrer'
          }
        : { to: url }
    },
    isExternalLink(url) {
      return typeof url === 'string' && /^(https?:)?\/\//.test(url)
    },
    handleScroll() {
      this.isScrolled = window.scrollY > 40
    }
  }
}
</script>

<style scoped>
.glass-premium {
  background: rgba(255, 255, 255, 0.7);
  backdrop-filter: blur(20px) saturate(180%);
  -webkit-backdrop-filter: blur(20px) saturate(180%);
  border-bottom: 1px solid rgba(255, 255, 255, 0.3);
}
</style>
