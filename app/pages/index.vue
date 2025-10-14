<template>
  <div>
    <!-- Hero Section -->
    <section id="home" class="min-h-screen flex items-center justify-center relative overflow-hidden bg-slate-50 dark:bg-slate-900">
      <!-- Simplified Background -->
      <div class="absolute inset-0 overflow-hidden">
        <div class="absolute top-20 left-10 w-96 h-96 bg-blue-500/5 rounded-full blur-3xl"></div>
        <div class="absolute bottom-20 right-10 w-96 h-96 bg-purple-500/5 rounded-full blur-3xl"></div>
      </div>

      <div class="container mx-auto px-6 relative z-10">
        <div class="max-w-6xl mx-auto">
          <!-- Modified layout with profile image on the right -->
          <div class="flex flex-col lg:flex-row items-center justify-between gap-12">
            <!-- Headline and Content -->
            <div class="flex-1 text-center lg:text-left space-y-8">
              <!-- Headline -->
              <div class="space-y-6">
                <h1 class="text-6xl md:text-8xl font-bold text-slate-900 dark:text-white leading-tight">
                  <span class="block">Hello!</span>
                  <span class="gradient-text block mt-2">Isma here</span>
                </h1>
                
                <div class="text-3xl md:text-5xl font-light text-slate-600 dark:text-slate-400 min-h-[60px] md:min-h-[80px] flex items-center lg:justify-start justify-center">
                  <div class="typewriter-container">
                    <span class="typewriter-text">{{ currentText }}</span>
                    <span class="typewriter-cursor">|</span>
                  </div>
                </div>
              </div>

              <!-- Description -->
              <p class="text-xl md:text-2xl text-slate-600 dark:text-slate-400 leading-relaxed max-w-2xl lg:max-w-none">
                Crafting <span class="text-blue-600 dark:text-blue-400 font-semibold">digital experiences</span> 
                with modern technologies and clean code.
              </p>

              <!-- CTA Buttons -->
              <div class="flex flex-col sm:flex-row gap-4 pt-8 lg:justify-start justify-center">
                <button 
                  class="px-8 py-4 bg-slate-900 dark:bg-white text-white dark:text-slate-900 rounded-2xl font-semibold transition-all duration-300 hover:scale-105 hover:shadow-2xl"
                  @click="openResume"
                >
                  View Resume
                </button>
                
                <button 
                  class="px-8 py-4 border-2 border-slate-300 dark:border-slate-600 text-slate-700 dark:text-slate-300 rounded-2xl font-semibold transition-all duration-300 hover:scale-105 hover:border-blue-500"
                  @click="scrollToSection('#contact')"
                >
                  Get In Touch
                </button>
              </div>
            </div>

            <!-- Profile Image - Now on the right -->
            <div class="flex-1 flex justify-center lg:justify-end">
              <div class="relative animate-float">
                <div class="w-60 h-60 md:w-80 md:h-80 rounded-3xl bg-gradient-to-br from-blue-500 to-purple-600 p-1.5 shadow-2xl">
                  <div class="w-full h-full rounded-2xl bg-white dark:bg-slate-900 overflow-hidden border-4 border-white dark:border-slate-800">
                    <img 
                      src="~/assets/ID.png" 
                      alt="Ismaliza Jaafar"
                      class="w-full h-full object-cover"
                    />
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Other Sections -->
    <AboutSection />
    <SkillsSection />
    <ProjectsSection />
    <ContactSection />
  </div>
</template>

<script setup>
import AboutSection from '~/components/AboutSection.vue'
import SkillsSection from '~/components/SkillsSection.vue'
import ProjectsSection from '~/components/ProjectsSection.vue'
import ContactSection from '~/components/ContactSection.vue'
import { ref, onMounted, onUnmounted } from 'vue'
import resumePDF from '~/assets/ismalizajaafar.pdf'

const texts = [
  'Software Engineer',
  'Web Developer',
  'Mobile Developer'
]

const currentText = ref('')
const currentIndex = ref(0)
const isDeleting = ref(false)
const typingSpeed = ref(100)
const pauseTime = ref(2000)

let timer = null

const typeWriter = () => {
  const fullText = texts[currentIndex.value]
  
  if (isDeleting.value) {
    // Deleting text
    currentText.value = fullText.substring(0, currentText.value.length - 1)
    typingSpeed.value = 50
  } else {
    // Typing text
    currentText.value = fullText.substring(0, currentText.value.length + 1)
    typingSpeed.value = 100
  }

  if (!isDeleting.value && currentText.value === fullText) {
    // Pause at end of typing
    typingSpeed.value = pauseTime.value
    isDeleting.value = true
  } else if (isDeleting.value && currentText.value === '') {
    // Move to next text after deleting
    isDeleting.value = false
    currentIndex.value = (currentIndex.value + 1) % texts.length
    typingSpeed.value = 500
  }

  timer = setTimeout(typeWriter, typingSpeed.value)
}

onMounted(() => {
  timer = setTimeout(typeWriter, 1000)
})

onUnmounted(() => {
  if (timer) {
    clearTimeout(timer)
  }
})

const scrollToSection = (sectionId) => {
  const element = document.querySelector(sectionId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}
const openResume = () => {
  window.open(resumePDF, '_blank')
}
</script>

<style>
.animate-float {
  animation: float 6s ease-in-out infinite;
}

.gradient-text {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.typewriter-container {
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

.typewriter-text {
  display: inline-block;
}

.typewriter-cursor {
  display: inline-block;
  margin-left: 2px;
  animation: blink 1s infinite;
  color: #667eea;
}

@keyframes float {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-20px); }
}

@keyframes blink {
  0%, 50% { opacity: 1; }
  51%, 100% { opacity: 0; }
}
</style>