<template>
  <section id="about" class="py-16 md:py-24 bg-slate-50 dark:bg-slate-900">
    <div class="container mx-auto px-4 sm:px-6"> <!-- MODIFY: Responsive padding -->
      <div class="max-w-6xl mx-auto">
        <!-- Section Header -->
        <div class="text-center mb-12 md:mb-20"> <!-- MODIFY: Responsive margin -->
          <!-- MODIFY: Responsive font sizes -->
          <h2 class="text-4xl sm:text-5xl md:text-6xl font-bold mb-4 md:mb-6 text-slate-900 dark:text-white">
            About <span class="gradient-text">Me</span>
          </h2>
          <!-- MODIFY: Responsive text size and padding -->
          <p class="text-lg sm:text-xl text-slate-600 dark:text-slate-400 max-w-2xl mx-auto leading-relaxed px-4 sm:px-0">
            Crafting digital experiences with clean code and innovative solutions
          </p>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 md:gap-16 items-center"> <!-- MODIFY: Responsive gap -->
          <!-- Content -->
          <div class="space-y-6 md:space-y-8"> <!-- MODIFY: Responsive spacing -->
            <!-- Introduction -->
            <div class="space-y-4 md:space-y-6"> <!-- MODIFY: Responsive spacing -->
              <!-- MODIFY: Responsive text sizes -->
              <p class="text-base sm:text-lg text-slate-700 dark:text-slate-300 leading-relaxed">
                I'm a passionate <span class="font-semibold text-blue-600 dark:text-blue-400">Fullstack Developer</span> with expertise in modern web technologies. 
                I specialize in creating scalable, user-friendly applications that solve real-world problems 
                and deliver exceptional user experiences.
              </p>
              
              <!-- <p class="text-base sm:text-lg text-slate-700 dark:text-slate-300 leading-relaxed">
                My journey in web development started with a curiosity about how digital products work, 
                and it has evolved into a passion for building solutions that make a difference. 
                I believe in writing <span class="font-semibold text-purple-600 dark:text-purple-400">clean, maintainable code</span> and following best practices 
                to ensure long-term project success.
              </p> -->

              <p class="text-base sm:text-lg text-slate-700 dark:text-slate-300 leading-relaxed">
                When I'm not coding, you can find me exploring new technologies, contributing to open-source projects, 
                or sharing knowledge with the developer community. I'm always eager to learn and take on new challenges 
                that push my boundaries.
              </p>
            </div>

            <!-- Key Focus Areas -->
            <!-- MODIFY: Responsive grid and spacing -->
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 md:gap-6 pt-4 md:pt-6">
              <div 
                v-for="focus in focusAreas"
                :key="focus.title"
                class="p-4 md:p-6 bg-white dark:bg-slate-800 rounded-xl md:rounded-2xl border border-slate-200 dark:border-slate-700 hover:border-blue-500/50 transition-all duration-300 group"
              >
                <!-- MODIFY: Responsive icon size -->
                <div class="text-xl md:text-2xl mb-2 md:mb-3 text-blue-600 dark:text-blue-400 group-hover:scale-110 transition-transform duration-300">
                  {{ focus.icon }}
                </div>
                <!-- MODIFY: Responsive text sizes -->
                <h3 class="font-semibold text-slate-900 dark:text-white mb-1 md:mb-2 text-base md:text-lg">
                  {{ focus.title }}
                </h3>
                <p class="text-slate-600 dark:text-slate-400 text-xs md:text-sm leading-relaxed">
                  {{ focus.description }}
                </p>
              </div>
            </div>
          </div>

          <!-- Visual Section -->
          <div class="relative">
            <!-- Main Content Card -->
            <!-- MODIFY: Responsive padding and rounding -->
            <div class="bg-white dark:bg-slate-800 rounded-2xl md:rounded-3xl p-6 md:p-8 border border-slate-200 dark:border-slate-700 shadow-lg">
              <!-- Tech Stack -->
              <div class="mb-6 md:mb-8">
                <!-- MODIFY: Responsive text size -->
                <h3 class="text-lg md:text-xl font-bold text-slate-900 dark:text-white mb-4 md:mb-6">Tech Stack</h3>
                <!-- MODIFY: Responsive gap and padding -->
                <div class="flex flex-wrap gap-2 md:gap-3">
                  <span 
                    v-for="tech in techStack"
                    :key="tech"
                    class="px-3 py-1 md:px-4 md:py-2 bg-slate-100 dark:bg-slate-700 text-slate-700 dark:text-slate-300 rounded-lg text-xs md:text-sm font-medium hover:bg-blue-100 dark:hover:bg-blue-900/30 hover:text-blue-700 dark:hover:text-blue-300 transition-all duration-300"
                  >
                    {{ tech }}
                  </span>
                </div>
              </div>

              <!-- Current Focus -->
              <div>
                <!-- MODIFY: Responsive text size -->
                <h3 class="text-lg md:text-xl font-bold text-slate-900 dark:text-white mb-3 md:mb-4">Currently Learning</h3>
                <div class="space-y-2 md:space-y-3">
                  <div 
                    v-for="item in currentLearning"
                    :key="item.name"
                    class="flex items-center space-x-2 md:space-x-3 p-2 md:p-3 bg-slate-50 dark:bg-slate-700/50 rounded-lg md:rounded-xl"
                  >
                    <!-- MODIFY: Responsive icon size -->
                    <span class="text-base md:text-lg">{{ item.icon }}</span>
                    <!-- MODIFY: Responsive text size -->
                    <span class="text-slate-700 dark:text-slate-300 font-medium text-sm md:text-base">{{ item.name }}</span>
                  </div>
                </div>
              </div>
            </div>

            <!-- Decorative Elements - Hide on mobile for better performance -->
            <!-- MODIFY: Hide decorative elements on mobile -->
            <div class="hidden md:block absolute -top-4 -right-4 w-16 md:w-24 h-16 md:h-24 bg-gradient-to-br from-blue-500 to-purple-600 rounded-2xl opacity-10 -z-10"></div>
            <div class="hidden md:block absolute -bottom-4 -left-4 w-12 md:w-20 h-12 md:h-20 bg-gradient-to-br from-green-500 to-blue-600 rounded-2xl opacity-10 -z-10"></div>
          </div>
        </div>

        <!-- Call to Action -->
        <!-- MODIFY: Responsive margin and button size -->
        <div class="text-center mt-12 md:mt-16">
          <button 
            @click="scrollToProjects"
            class="bg-slate-900 dark:bg-white text-white dark:text-slate-900 px-6 py-3 md:px-8 md:py-4 rounded-xl md:rounded-2xl font-semibold transition-all duration-300 hover:scale-105 hover:shadow-2xl border border-slate-200 dark:border-slate-700 group text-sm md:text-base"
          >
            <span class="flex items-center space-x-2 md:space-x-3">
              <span>View My Work</span>
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
const focusAreas = [
  {
    icon: '⚡',
    title: 'Frontend Development',
    description: 'Creating responsive, interactive user interfaces with modern frameworks like Vue.js and React'
  },
  {
    icon: '🛠️',
    title: 'Backend Development',
    description: 'Building scalable server-side applications and APIs with Node.js and Python'
  },
  {
    icon: '🎨',
    title: 'UI/UX Design',
    description: 'Designing intuitive user experiences with clean, modern interfaces using Tailwind CSS'
  },
  {
    icon: '🚀',
    title: 'Performance Optimization',
    description: 'Optimizing applications for speed, efficiency, and better user experience'
  }
]

const techStack = [
  'Vue.js', 'Nuxt.js', 'React', 'TypeScript', 
  'Node.js', 'Python', 'Tailwind CSS', 'MongoDB',
  'MySQL', 'Git', 'Docker', 'AWS'
]

const currentLearning = [
  { name: 'ReactJS', icon: '🔷' },
  { name: 'Cloud Architecture', icon: '☁️' },
  { name: 'Data Analyst', icon: '🏗️' }
]

const scrollToProjects = () => {
  const element = document.querySelector('#projects')
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
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
</style>