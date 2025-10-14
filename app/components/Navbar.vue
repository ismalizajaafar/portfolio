<template>
  <nav 
    class="fixed top-4 sm:top-6 left-1/2 transform -translate-x-1/2 z-50 transition-all duration-300 w-[90%] max-w-md" 
    :class="scrolled ? 'scale-95' : 'scale-100'"
  >
    <!-- Floating Navbar Container -->
    <div class="glass rounded-full px-4 py-2 sm:px-6 sm:py-3 border border-slate-700/50 backdrop-blur-xl w-full">
      <div class="flex items-center justify-center"> <!-- MODIFY: Center content -->
        <!-- Navigation Items - Centered -->
        <div class="flex items-center space-x-4 sm:space-x-6 md:space-x-8"> <!-- MODIFY: Adjusted spacing -->
          <a 
            v-for="item in navItems" 
            :key="item.name"
            :href="item.href"
            class="text-slate-300 hover:text-white transition-all duration-300 text-xs sm:text-sm font-medium relative group"
            @click.prevent="scrollToSection(item.href)"
            :class="activeSection === item.href.slice(1) ? 'text-white' : ''"
          >
            <span class="relative z-10">{{ item.name }}</span>
            <!-- Active indicator -->
            <span 
              v-if="activeSection === item.href.slice(1)"
              class="absolute -bottom-1 left-0 w-full h-0.5 bg-gradient-to-r from-blue-500 to-purple-600 rounded-full"
            ></span>
            <!-- Hover indicator -->
            <span class="absolute -bottom-1 left-0 w-0 h-0.5 bg-gradient-to-r from-blue-500 to-purple-600 rounded-full transition-all duration-300 group-hover:w-full"></span>
          </a>
        </div>
      </div>
    </div>
  </nav>
</template>

<script setup>
const scrolled = ref(false)
const activeSection = ref('home')

const navItems = [
  { name: 'Home', href: '#home' },
  { name: 'About', href: '#about' },
  { name: 'Skills', href: '#skills' },
  { name: 'Projects', href: '#projects' },
  { name: 'Contact', href: '#contact' }
]

const handleScroll = () => {
  scrolled.value = window.scrollY > 100
  
  // Update active section based on scroll position
  const sections = ['home', 'about', 'skills', 'projects', 'contact']
  const scrollPosition = window.scrollY + 100

  for (const section of sections) {
    const element = document.getElementById(section)
    if (element) {
      const offsetTop = element.offsetTop
      const offsetBottom = offsetTop + element.offsetHeight
      
      if (scrollPosition >= offsetTop && scrollPosition < offsetBottom) {
        activeSection.value = section
        break
      }
    }
  }
}

const scrollToSection = (sectionId) => {
  const element = document.querySelector(sectionId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
    // Update active section immediately
    activeSection.value = sectionId.slice(1)
  }
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  // Set initial active section
  handleScroll()
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
.glass {
  background: rgba(15, 23, 42, 0.9);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.1);
}

/* Mobile optimizations */
@media (max-width: 640px) {
  .glass {
    backdrop-filter: blur(16px);
  }
}
</style>