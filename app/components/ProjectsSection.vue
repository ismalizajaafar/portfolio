<template>
  <section id="projects" class="py-16 md:py-24 bg-slate-50 dark:bg-slate-900">
    <div class="container mx-auto px-4 sm:px-6"> <!-- MODIFY: Responsive padding -->
      <div class="max-w-7xl mx-auto">
        <!-- Section Header -->
        <div class="text-center mb-12 md:mb-20"> <!-- MODIFY: Responsive margin -->
          <!-- MODIFY: Responsive font sizes -->
          <h2 class="text-4xl sm:text-5xl md:text-6xl font-bold mb-4 md:mb-6 text-slate-900 dark:text-white">
            Featured <span class="gradient-text">Projects</span>
          </h2>
          <!-- MODIFY: Responsive text size and padding -->
          <p class="text-lg sm:text-xl text-slate-600 dark:text-slate-400 max-w-2xl mx-auto leading-relaxed px-4 sm:px-0">
            A collection of projects that showcase my skills in full-stack development and problem-solving
          </p>
        </div>

        <!-- Projects Grid -->
        <!-- MODIFY: Responsive grid and gap -->
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-6 md:gap-8">
          <div 
            v-for="project in projects"
            :key="project.id"
            class="group bg-white dark:bg-slate-800 rounded-2xl md:rounded-3xl overflow-hidden border border-slate-200 dark:border-slate-700 shadow-sm hover:shadow-2xl transition-all duration-500 hover:scale-105"
          >
            <!-- Project Image Container -->
            <div class="relative overflow-hidden">
              <img 
                :src="project.image" 
                :alt="project.title"
                class="w-full h-48 sm:h-56 md:h-64 object-cover transform group-hover:scale-110 transition-transform duration-700" >
              
        
              <div class="absolute inset-0 bg-gradient-to-t from-slate-900/80 via-slate-900/20 to-transparent opacity-60 group-hover:opacity-30 transition-opacity duration-500"></div>
              
              <!-- Status Badge -->
              <!-- MODIFY: Responsive positioning and padding -->
              <div class="absolute top-4 right-4 md:top-6 md:right-6">
                <span 
                  class="px-3 py-1 md:px-4 md:py-2 rounded-full text-xs md:text-sm font-semibold backdrop-blur-md border"
                  :class="getStatusClass(project.status)"
                >
                  {{ project.status }}
                </span>
              </div>

              <!-- Project Info Overlay -->
              <!-- MODIFY: Responsive positioning and text sizes -->
              <div class="absolute bottom-4 left-4 right-4 md:bottom-6 md:left-6 md:right-6">
                <h3 class="text-xl md:text-2xl font-bold text-white mb-1 md:mb-2 group-hover:translate-y-1 transition-transform duration-500">
                  {{ project.title }}
                </h3>
                <p class="text-slate-200 text-xs md:text-sm leading-relaxed opacity-90 group-hover:opacity-100 transition-opacity duration-500 line-clamp-2">
                  {{ project.description }}
                </p>
              </div>
            </div>

            <!-- Project Content -->
            <!-- MODIFY: Responsive padding -->
            <div class="p-4 md:p-6 lg:p-8">
              <!-- Technologies -->
              <div class="flex flex-wrap-center gap-2 md:gap-3 mb-4 md:mb-6"> <!-- MODIFY: Responsive gap and margin -->
                <span 
                  v-for="tech in project.technologies" 
                  :key="tech"
                  class="px-2 py-1 md:px-3 md:py-2 bg-slate-100 dark:bg-slate-700 text-slate-700 dark:text-slate-300 rounded-lg text-xs md:text-sm font-medium transition-all duration-300 hover:bg-blue-100 dark:hover:bg-blue-900/30 hover:text-blue-700 dark:hover:text-blue-300"
                >
                  {{ tech }}
                </span>
              </div>

              <!-- Project Links -->
              <!-- MODIFY: Responsive layout and sizing -->
              <div class="flex flex-col sm:flex-row gap-3 md:gap-4"> <!-- MODIFY: Stack on mobile -->
                <button 
                  class="flex-1 bg-slate-900 dark:bg-white text-white dark:text-slate-900 px-4 py-2 md:px-6 md:py-3 rounded-lg md:rounded-xl font-semibold transition-all duration-300 hover:scale-105 hover:shadow-lg flex items-center justify-center space-x-2 md:space-x-3 group/link text-sm md:text-base"
                  @click="openDemo(project.demoUrl)"
                >
                  <span>Live Demo</span>
                  <svg class="w-3 h-3 md:w-4 md:h-4 transform group-hover/link:translate-x-1 transition-transform duration-300" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"></path>
                  </svg>
                </button>
                <!-- <button 
                  class="flex-1 border-2 border-slate-300 dark:border-slate-600 text-slate-700 dark:text-slate-300 px-4 py-2 md:px-6 md:py-3 rounded-lg md:rounded-xl font-semibold transition-all duration-300 hover:scale-105 hover:border-slate-400 dark:hover:border-slate-500 hover:bg-slate-50 dark:hover:bg-slate-700 flex items-center justify-center space-x-2 md:space-x-3 group/link text-sm md:text-base"
                  @click="openGithub(project.githubUrl)"
                >
                  <span>Source Code</span>
                  <svg class="w-3 h-3 md:w-4 md:h-4 transform group-hover/link:translate-x-1 transition-transform duration-300" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4"></path>
                  </svg>
                </button> -->
              </div>
            </div>
          </div>
        </div>

        <!-- View More Projects -->
        <!-- MODIFY: Responsive margin and button size -->
        <div class="text-center mt-12 md:mt-16">
          <button class="bg-white dark:bg-slate-800 text-slate-900 dark:text-white px-6 py-3 md:px-8 md:py-4 rounded-xl md:rounded-2xl font-semibold transition-all duration-300 hover:scale-105 hover:shadow-2xl border border-slate-200 dark:border-slate-700 group text-sm md:text-base">
            <span class="flex items-center space-x-2 md:space-x-3">
              <span>View All Projects</span>
              <svg class="w-4 h-4 md:w-5 md:h-5 transform group-hover:translate-x-1 md:group-hover:translate-x-2 transition-transform duration-300" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3"></path>
              </svg>
            </span>
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const projects = [
  {
    id: 1,
    title: 'Commmerce Landing Page',
    description: 'Company Landing page with email hosting and SEO optimization.',
    image: 'https://images.unsplash.com/photo-1556742049-0cfed4f6a45d?w=600&h=400&fit=crop',
    technologies: ['Vue.js', 'Nuxt', 'Node.js'],
    status: 'Live',
    demoUrl: 'https://merdekanetwork.com/',
    githubUrl: '#'
  }
]

const getStatusClass = (status) => {
  switch (status) {
    case 'Live':
      return 'bg-green-500/90 text-white border-green-600 shadow-lg shadow-green-500/25'
    case 'In Progress':
      return 'bg-yellow-500/90 text-white border-yellow-600 shadow-lg shadow-yellow-500/25'
    case 'Coming Soon':
      return 'bg-blue-500/90 text-white border-blue-600 shadow-lg shadow-blue-500/25'
    default:
      return 'bg-slate-500/90 text-white border-slate-600'
  }
}

const openDemo = (url) => {
  if (url !== '#') {
    window.open(url, '_blank')
  } else {
    // Show coming soon message
    alert('Demo coming soon! 🚀')
  }
}

const openGithub = (url) => {
  if (url !== '#') {
    window.open(url, '_blank')
  } else {
    // Show coming soon message
    alert('Source code will be available soon! 💻')
  }
}
</script>

<style scoped>
.gradient-text {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  background-size: 200% 200%;
  animation: gradient 6s ease infinite;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

@keyframes gradient {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

/* Mobile optimizations */
@media (max-width: 640px) {
  .gradient-text {
    font-size: inherit; /* Ensure gradient text scales properly */
  }
}

/* Line clamp utility for description text */
.line-clamp-2 {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
</style>