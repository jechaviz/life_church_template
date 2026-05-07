<template>
  <footer class="bg-[#050608] text-white pt-32 pb-16 border-t border-white/5 relative overflow-hidden">
    <!-- Subtle Background Glow -->
    <div class="absolute top-0 left-1/2 -translate-x-1/2 w-full h-px bg-gradient-to-r from-transparent via-orange-600/50 to-transparent"></div>

    <div class="max-w-7xl mx-auto px-8 sm:px-10 lg:px-12 relative z-10">
      <div class="grid grid-cols-2 lg:grid-cols-5 gap-16 mb-24">

        <!-- Brand Identity Column -->
        <div class="col-span-2 space-y-8">
          <a href="https://www.life.church/" class="flex items-center gap-3 group">
             <div class="w-12 h-12 bg-white/5 rounded-2xl flex items-center justify-center border border-white/10 group-hover:bg-orange-600/10 transition-colors">
               <i class="fa-solid fa-shapes text-orange-600 text-2xl"></i>
             </div>
             <span class="font-black text-2xl tracking-[-0.05em]">LIFE.CHURCH</span>
          </a>
          <p class="text-sm text-gray-400 font-light leading-relaxed max-w-sm">
            We exist to lead people to become fully devoted followers of Christ. This is the passion behind everything we do.
          </p>

          <!-- Socials with Glowing Hover -->
          <div class="flex items-center gap-4">
            <a v-for="social in footer.socialLinks" :key="social.url" :href="social.url" target="_blank" rel="noopener noreferrer" :aria-label="getSocialLabel(social.type)"
               class="w-10 h-10 bg-white/5 hover:bg-white/10 rounded-xl flex items-center justify-center text-gray-400 hover:text-orange-500 border border-white/5 transition-all duration-500 hover:scale-110 active:scale-95 group">
              <i :class="['fa-brands', getSocialIcon(social.type), 'text-lg group-hover:drop-shadow-[0_0_8px_rgba(255,90,0,0.5)]']"></i>
            </a>
          </div>
        </div>

        <!-- Navigation Columns (Generated from siteData) -->
        <div class="col-span-2 lg:col-span-3 grid grid-cols-2 md:grid-cols-3 gap-12">
          <div class="space-y-8">
            <h4 class="text-[10px] font-black uppercase tracking-[0.4em] text-orange-600">Explore</h4>
            <ul class="space-y-4">
              <li v-for="link in footer.navLinks.slice(0, 4)" :key="link.title">
                <component :is="getFooterLinkComponent(link.url)" v-bind="getFooterLinkAttrs(link.url)" class="text-sm font-medium text-gray-400 hover:text-white transition-colors flex items-center gap-2 group">
                  <span class="w-0 h-px bg-orange-600 transition-all duration-500 group-hover:w-3"></span>
                  {{ link.title }}
                </component>
              </li>
            </ul>
          </div>
          <div class="space-y-8">
            <h4 class="text-[10px] font-black uppercase tracking-[0.4em] text-orange-600">Quick Links</h4>
            <ul class="space-y-4">
              <li v-for="link in footer.navLinks.slice(4)" :key="link.title">
                <component :is="getFooterLinkComponent(link.url)" v-bind="getFooterLinkAttrs(link.url)" class="text-sm font-medium text-gray-400 hover:text-white transition-colors flex items-center gap-2 group">
                  <span class="w-0 h-px bg-orange-600 transition-all duration-500 group-hover:w-3"></span>
                  {{ link.title }}
                </component>
              </li>
            </ul>
          </div>
          <div class="space-y-8">
            <h4 class="text-[10px] font-black uppercase tracking-[0.4em] text-orange-600">Stay Connected</h4>
            <div class="flex flex-col items-start gap-4">
              <router-link to="/contact" class="inline-flex items-center gap-3 text-sm font-bold text-gray-300 hover:text-white">
                Contact Us
                <i class="fa-solid fa-arrow-right text-[10px] text-orange-600"></i>
              </router-link>
              <a href="https://live.life.church/" target="_blank" rel="noopener noreferrer" class="inline-flex items-center gap-3 text-sm font-bold text-gray-300 hover:text-white">
                Church Online
                <i class="fa-solid fa-arrow-up-right-from-square text-[10px] text-orange-600"></i>
              </a>
            </div>
            <p class="text-[10px] text-gray-500 leading-relaxed font-medium">Use a real path for support, prayer, locations, and online services.</p>
          </div>
        </div>

      </div>

      <!-- Legal & Credits -->
      <div class="pt-16 border-t border-white/5 flex flex-col md:flex-row justify-between items-center gap-8">
        <div class="flex flex-wrap justify-center md:justify-start gap-x-8 gap-y-4">
          <a v-for="policy in policies" :key="policy.name" :href="policy.url" class="text-[10px] font-black uppercase tracking-[0.2em] text-gray-500 hover:text-white transition-colors">
            {{ policy.name }}
          </a>
        </div>
        <p class="text-[10px] font-black uppercase tracking-[0.2em] text-gray-600">
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
      footer: window.siteData.footer,
      policies: [
        { name: 'Privacy Policy', url: 'https://www.life.church/privacy/' },
        { name: 'Terms of Use', url: 'https://www.life.church/terms/' },
        { name: 'Vulnerability Program', url: 'https://www.life.church/vulnerability-disclosure-program/' }
      ]
    }
  },
  methods: {
    isExternalUrl(url) {
      return /^(https?:)?\/\//.test(url) || /^(mailto|tel):/.test(url);
    },
    getFooterLinkComponent(url) {
      return this.isExternalUrl(url) ? 'a' : 'router-link';
    },
    getFooterLinkAttrs(url) {
      return this.isExternalUrl(url) ? { href: url } : { to: url };
    },
    getSocialIcon(type) {
      const icons = {
        'icon-facebook': 'fa-facebook-f',
        'icon-instagram': 'fa-instagram',
        'icon-tiktok': 'fa-tiktok',
        'icon-youtube': 'fa-youtube',
        'icon-linkedin': 'fa-linkedin-in'
      };
      return icons[type] || 'fa-link';
    },
    getSocialLabel(type) {
      const labels = {
        'icon-facebook': 'Life.Church on Facebook',
        'icon-instagram': 'Life.Church on Instagram',
        'icon-tiktok': 'Life.Church on TikTok',
        'icon-youtube': 'Life.Church on YouTube',
        'icon-linkedin': 'Life.Church on LinkedIn'
      };
      return labels[type] || 'Life.Church social link';
    }
  }
}
</script>
