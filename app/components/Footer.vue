<template>
  <footer class="bg-slate-900 border-t border-slate-800 py-12 md:py-16"> <!-- MODIFY: Responsive padding -->
    <div class="container mx-auto px-4 sm:px-6"> <!-- MODIFY: Responsive padding -->
      <div class="max-w-6xl mx-auto">
        <!-- Main Footer Content -->
        <!-- MODIFY: Responsive grid and spacing -->
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 md:gap-8 mb-8 md:mb-12">
          <!-- Brand Column -->
          <div class="md:col-span-2 lg:col-span-2">
            <div class="flex items-center space-x-3 mb-4 md:mb-6">
              <!-- MODIFY: Responsive logo size -->
              <div class="w-8 h-8 md:w-10 md:h-10 bg-gradient-to-br from-blue-500 to-purple-600 rounded-lg md:rounded-xl flex items-center justify-center">
                <span class="text-white font-bold text-xs md:text-sm">IJ</span>
              </div>
              <!-- MODIFY: Responsive text size -->
              <span class="text-xl md:text-2xl font-bold text-white">Ismaliza Jaafar</span>
            </div>
            <!-- MODIFY: Responsive text size -->
            <p class="text-slate-400 text-base md:text-lg leading-relaxed max-w-md">
              Fullstack developer passionate about creating exceptional digital experiences through clean code and innovative solutions.
            </p>
          </div>

          <!-- Quick Links -->
          <div>
            <!-- MODIFY: Responsive text size -->
            <h3 class="text-white font-semibold text-base md:text-lg mb-4 md:mb-6">Navigation</h3>
            <div class="space-y-2 md:space-y-4"> <!-- MODIFY: Responsive spacing -->
              <a 
                v-for="item in navItems"
                :key="item.name"
                :href="item.href"
                class="block text-slate-400 hover:text-white transition-colors duration-300 text-sm md:text-sm"
                @click.prevent="scrollToSection(item.href)"
              >
                {{ item.name }}
              </a>
            </div>
          </div>

          <!-- Connect -->
          <div>
            <!-- MODIFY: Responsive text size -->
            <h3 class="text-white font-semibold text-base md:text-lg mb-4 md:mb-6">Let's Connect</h3>
            <!-- MODIFY: Responsive text size and margin -->
            <p class="text-slate-400 text-xs md:text-sm mb-4 md:mb-6 leading-relaxed">
              Interested in working together? Let's talk about your next project.
            </p>
            <div class="flex space-x-3 md:space-x-4"> <!-- MODIFY: Responsive spacing -->
              <a 
                v-for="social in socialLinks"
                :key="social.name"
                :href="social.url"
                class="w-10 h-10 md:w-12 md:h-12 bg-slate-800 hover:bg-slate-700 rounded-lg md:rounded-xl flex items-center justify-center text-slate-400 hover:text-white transition-all duration-300 transform hover:scale-110 group"
                :title="social.name"
              >
                <!-- MODIFY: Responsive icon size -->
                <span class="text-lg md:text-xl group-hover:scale-110 transition-transform duration-300">{{ social.icon }}</span>
              </a>
            </div>
          </div>
        </div>

        <!-- Bottom Bar -->
        <div class="border-t border-slate-800 pt-6 md:pt-8"> <!-- MODIFY: Responsive padding -->
          <div class="flex flex-col md:flex-row justify-between items-center space-y-4 md:space-y-0">
            <!-- Copyright -->
            <!-- MODIFY: Responsive text size and alignment -->
            <div class="text-slate-400 text-xs md:text-sm text-center md:text-left order-2 md:order-1">
              <p>&copy; 2025 Ismaliza Jaafar. All rights reserved.</p>
            </div>

            <!-- Additional Links -->
            <!-- MODIFY: Responsive spacing and order -->
            <div class="flex space-x-4 md:space-x-6 text-slate-400 text-xs md:text-sm order-1 md:order-2">
              <a href="#" class="hover:text-white transition-colors duration-300">Privacy Policy</a>
              <a href="#" class="hover:text-white transition-colors duration-300">Terms of Service</a>
            </div>

            <!-- Back to Top -->
            <!-- MODIFY: Responsive size and order -->
            <button 
              @click="scrollToTop"
              class="flex items-center space-x-2 text-slate-400 hover:text-white transition-colors duration-300 group order-3 text-xs md:text-sm"
            >
              <span class="hidden sm:inline">Back to top</span> <!-- MODIFY: Hide text on mobile -->
              <span class="sm:hidden">Top</span> <!-- MODIFY: Shorter text for mobile -->
              <svg class="w-3 h-3 md:w-4 md:h-4 transform group-hover:-translate-y-1 transition-transform duration-300" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 10l7-7m0 0l7 7m-7-7v18"></path>
              </svg>
            </button>
          </div>
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup>
const socialLinks = [
  { name: 'LinkedIn', icon: '💼', url: 'https://linkedin.com/in/ismaliza-jaafar' },
  { name: 'GitHub', icon: '🐙', url: 'https://github.com/ismalizajaafar' },
  { name: 'Email', icon: '📧', url: 'mailto:ismalizajaafar@gmail.com' } 
]

const navItems = [
  { name: 'Home', href: '#home' },
  { name: 'About', href: '#about' },
  { name: 'Skills', href: '#skills' },
  { name: 'Projects', href: '#projects' },
  { name: 'Contact', href: '#contact' }
]

const scrollToSection = (sectionId) => {
  const element = document.querySelector(sectionId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}
</script>