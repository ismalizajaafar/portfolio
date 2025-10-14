<template>
  <section id="skills" class="py-16 md:py-24 bg-slate-50 dark:bg-slate-900">
    <div class="container mx-auto px-4 sm:px-6"> <!-- MODIFY: Responsive padding -->
      <div class="max-w-6xl mx-auto">
        <!-- Section Header -->
        <div class="text-center mb-12 md:mb-20"> <!-- MODIFY: Responsive margin -->
          <!-- MODIFY: Responsive font sizes -->
          <h2 class="text-4xl sm:text-5xl md:text-6xl font-bold mb-4 md:mb-6 text-slate-900 dark:text-white">
            Technologies & <span class="gradient-text">Tools</span>
          </h2>
          <!-- MODIFY: Responsive text size and padding -->
          <p class="text-lg sm:text-xl text-slate-600 dark:text-slate-400 max-w-2xl mx-auto leading-relaxed px-4 sm:px-0">
            A curated stack of modern technologies I work with to build exceptional digital experiences
          </p>
        </div>

        <!-- Skills Grid -->
        <!-- MODIFY: Responsive grid columns and gap -->
        <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-6 gap-4 md:gap-6 lg:gap-8">
          <div 
            v-for="(skill) in skills"
            :key="skill.name"
            class="group relative"
          >
            <!-- MODIFY: Responsive padding and rounding -->
            <div class="aspect-square bg-white dark:bg-slate-800 rounded-xl md:rounded-2xl border border-slate-200 dark:border-slate-700 shadow-sm hover:shadow-xl transition-all duration-500 group-hover:scale-105 group-hover:-translate-y-1 md:group-hover:-translate-y-2 flex flex-col items-center justify-center p-3 md:p-4 lg:p-6 relative overflow-hidden">
              
              <!-- Background Gradient on Hover -->
              <div class="absolute inset-0 bg-gradient-to-br from-blue-50 to-purple-50 dark:from-blue-900/10 dark:to-purple-900/10 opacity-0 group-hover:opacity-100 transition-opacity duration-500"></div>
              
              <!-- Skill Icon -->
              <!-- MODIFY: Responsive icon size -->
              <div class="text-2xl sm:text-3xl md:text-4xl mb-2 md:mb-3 lg:mb-4 text-slate-700 dark:text-slate-300 group-hover:text-slate-900 dark:group-hover:text-white transition-colors duration-500 relative z-10">
                {{ skill.icon }}
              </div>
              
              <!-- Skill Name -->
              <!-- MODIFY: Responsive text size -->
              <h3 class="font-semibold text-slate-800 dark:text-slate-200 group-hover:text-slate-900 dark:group-hover:text-white transition-colors duration-500 text-xs sm:text-sm text-center relative z-10 leading-tight">
                {{ skill.name }}
              </h3>

              <!-- Category Badge -->
              <!-- MODIFY: Responsive positioning and size -->
              <div class="absolute top-2 right-2 md:top-3 md:right-3">
                <span class="text-[10px] xs:text-xs px-1.5 py-0.5 md:px-2 md:py-1 rounded-full bg-slate-100 dark:bg-slate-700 text-slate-600 dark:text-slate-400 font-medium">
                  {{ skill.category }}
                </span>
              </div>
            </div>
          </div>
        </div>

        <!-- Tech Stack Categories -->
        <!-- MODIFY: Responsive margin, grid, and padding -->
        <div class="mt-12 md:mt-16 lg:mt-20 grid grid-cols-1 md:grid-cols-3 gap-6 md:gap-8">
          <div 
            v-for="category in categories"
            :key="category.name"
            class="text-center p-6 md:p-8 rounded-xl md:rounded-2xl bg-gradient-to-br from-white to-slate-50 dark:from-slate-800 dark:to-slate-900 border border-slate-200 dark:border-slate-700"
          >
            <!-- MODIFY: Responsive icon size -->
            <div class="text-2xl md:text-3xl mb-3 md:mb-4 text-slate-600 dark:text-slate-400">
              {{ category.icon }}
            </div>
            <!-- MODIFY: Responsive text sizes -->
            <h3 class="text-lg md:text-xl font-bold text-slate-900 dark:text-white mb-2 md:mb-3">
              {{ category.name }}
            </h3>
            <p class="text-slate-600 dark:text-slate-400 text-xs md:text-sm leading-relaxed">
              {{ category.description }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const skills = [
  // Frontend
  { name: 'Vue.js', icon: '⚡', category: 'Frontend' },
  { name: 'Nuxt.js', icon: '🚀', category: 'Frontend' },
  { name: 'React', icon: '⚛️', category: 'Frontend' },
  { name: 'TypeScript', icon: '🔷', category: 'Frontend' },
  { name: 'Tailwind', icon: '🎨', category: 'Frontend' },
  
  // Backend
  { name: 'Node.js', icon: '🟢', category: 'Backend' },
  { name: 'MySQL', icon: '🐘', category: 'Backend' },
  { name: 'Linux', icon: '🍃', category: 'Backend' },
  
  // Tools & DevOps
  { name: 'Git', icon: '📚', category: 'Tools' },
  { name: 'Docker', icon: '🐳', category: 'Tools' },
  { name: 'AWS', icon: '☁️', category: 'Tools' },
  { name: 'Vercel', icon: '▲', category: 'Tools' },
  { name: 'Figma', icon: '🎯', category: 'Tools' }
]

const categories = [
  {
    name: 'Frontend',
    icon: '💻',
    description: 'Modern frameworks and libraries for building responsive, interactive user interfaces'
  },
  {
    name: 'Backend',
    icon: '⚙️',
    description: 'Server-side technologies and databases for building scalable, efficient applications'
  },
  {
    name: 'Tools & DevOps',
    icon: '🛠️',
    description: 'Development tools, deployment platforms, and infrastructure management'
  }
]
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

/* Staggered animation for skills - Reduced on mobile for performance */
.group {
  animation: fadeUp 0.6s ease-out forwards;
  opacity: 0;
}

@keyframes fadeUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Mobile optimizations */
@media (max-width: 640px) {
  .gradient-text {
    font-size: inherit; /* Ensure gradient text scales properly */
  }
  
  /* Reduce animation intensity on mobile */
  .group:hover .aspect-square {
    transform: scale(1.02) translateY(-1px);
  }
}

/* Extra small screen optimizations */
@media (max-width: 375px) {
  .grid-cols-2 {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}
</style>