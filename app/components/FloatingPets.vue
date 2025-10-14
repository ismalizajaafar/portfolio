<template>
  <div 
    ref="petContainer"
    class="fixed z-40 cursor-pointer transition-all duration-1000 ease-linear"
    :style="{
      left: position.x + 'px',
      top: position.y + 'px',
      transform: `scale(${isHovered ? 1.2 : 1}) rotateY(${velocity.x > 0 ? '0deg' : '180deg'})`
    }"
    @mouseenter="isHovered = true"
    @mouseleave="isHovered = false"
    @click="interactWithPet"
  >
    <!-- Shiba Inu Character -->
    <div class="relative">
      <!-- Body -->
      <div class="w-16 h-12 bg-gradient-to-br from-amber-400 to-orange-500 rounded-full shadow-lg border-2 border-white dark:border-slate-800 relative overflow-hidden">
        <!-- White chest -->
        <div class="absolute bottom-0 left-1/2 transform -translate-x-1/2 w-10 h-6 bg-white rounded-t-full"></div>
      </div>
      
      <!-- Head -->
      <div class="absolute -top-4 left-1/2 transform -translate-x-1/2 w-14 h-14 bg-gradient-to-br from-amber-400 to-orange-500 rounded-full border-2 border-white dark:border-slate-800">
        <!-- Snout -->
        <div class="absolute bottom-2 left-1/2 transform -translate-x-1/2 w-8 h-6 bg-amber-100 rounded-full"></div>
        
        <!-- Eyes -->
        <div class="absolute top-4 left-3 w-2 h-2 bg-black rounded-full"></div>
        <div class="absolute top-4 right-3 w-2 h-2 bg-black rounded-full"></div>
        
        <!-- Eyebrows -->
        <div class="absolute top-2 left-2 w-3 h-1 bg-amber-600 rounded-full rotate-12"></div>
        <div class="absolute top-2 right-2 w-3 h-1 bg-amber-600 rounded-full -rotate-12"></div>
        
        <!-- Nose -->
        <div class="absolute bottom-3 left-1/2 transform -translate-x-1/2 w-2 h-1 bg-black rounded-full"></div>
        
        <!-- Ears -->
        <div class="absolute -top-1 left-1 w-4 h-6 bg-amber-600 rounded-full rotate-12"></div>
        <div class="absolute -top-1 right-1 w-4 h-6 bg-amber-600 rounded-full -rotate-12"></div>
        
        <!-- Inner Ears -->
        <div class="absolute top-1 left-2 w-2 h-4 bg-amber-200 rounded-full rotate-12"></div>
        <div class="absolute top-1 right-2 w-2 h-4 bg-amber-200 rounded-full -rotate-12"></div>
      </div>

      <!-- Tail -->
      <div class="absolute -right-2 top-2 w-6 h-3 bg-amber-500 rounded-full rotate-45"></div>
      
      <!-- Paws -->
      <div class="absolute -bottom-1 left-2 w-3 h-2 bg-amber-500 rounded-full"></div>
      <div class="absolute -bottom-1 right-2 w-3 h-2 bg-amber-500 rounded-full"></div>
      
      <!-- Floating Effect -->
      <div class="absolute -inset-2 bg-amber-300 rounded-full opacity-20 animate-ping"></div>
    </div>

    <!-- Speech Bubble -->
    <div 
      v-if="showMessage"
      class="absolute -top-20 left-1/2 transform -translate-x-1/2 bg-white dark:bg-slate-800 px-3 py-2 rounded-2xl shadow-lg text-xs font-medium text-slate-900 dark:text-white whitespace-nowrap border border-slate-200 dark:border-slate-600"
    >
      {{ currentMessage }}
      <div class="absolute bottom-0 left-1/2 transform -translate-x-1/2 translate-y-1 w-2 h-2 bg-white dark:bg-slate-800 rotate-45 border-r border-b border-slate-200 dark:border-slate-600"></div>
    </div>

    <!-- Trail Effect -->
    <div 
      v-for="(trail, index) in trails"
      :key="index"
      class="absolute w-2 h-2 bg-amber-200 rounded-full opacity-0 animate-fade-out"
      :style="{
        left: trail.x + 'px',
        top: trail.y + 'px'
      }"
    ></div>
  </div>
</template>

<script setup>
const petContainer = ref(null)
const position = ref({ x: 100, y: 100 })
const velocity = ref({ x: 1, y: 1 })
const isHovered = ref(false)
const showMessage = ref(false)
const currentMessage = ref('')
const trails = ref([])

const messages = [
  'Woof! 🐕',
  'Such portfolio!',
  'Very code! 🎯',
  'Much skills!',
  'Wow! Amazing! 🌟',
  'Let\'s play! 🎾',
  'Good human! 👋',
  'Shiba approved! ✅'
]

const movePet = () => {
  if (isHovered.value) return

  const newX = position.value.x + velocity.value.x
  const newY = position.value.y + velocity.value.y

  // Boundary checking - increased size for Shiba
  const maxX = window.innerWidth - 64
  const maxY = window.innerHeight - 64

  if (newX <= 0 || newX >= maxX) {
    velocity.value.x *= -1
    addTrail()
  }
  if (newY <= 0 || newY >= maxY) {
    velocity.value.y *= -1
    addTrail()
  }

  position.value.x = Math.max(0, Math.min(newX, maxX))
  position.value.y = Math.max(0, Math.min(newY, maxY))

  // Occasionally change direction
  if (Math.random() < 0.02) {
    velocity.value.x = (Math.random() - 0.5) * 3
    velocity.value.y = (Math.random() - 0.5) * 3
    addTrail()
  }

  // Add trail occasionally
  if (Math.random() < 0.3) {
    addTrail()
  }
}

const addTrail = () => {
  trails.value.push({
    x: Math.random() * 40 - 20,
    y: Math.random() * 40 - 20,
    id: Date.now() + Math.random()
  })

  // Limit trails
  if (trails.value.length > 5) {
    trails.value.shift()
  }
}

const interactWithPet = () => {
  // Change direction on click
  velocity.value.x = (Math.random() - 0.5) * 4
  velocity.value.y = (Math.random() - 0.5) * 4
  
  // Show random message
  showMessage.value = true
  currentMessage.value = messages[Math.floor(Math.random() * messages.length)]
  
  // Add multiple trails
  for (let i = 0; i < 8; i++) {
    setTimeout(() => addTrail(), i * 50)
  }

  // Hide message after 3 seconds
  setTimeout(() => {
    showMessage.value = false
  }, 3000)
}

// Auto-interaction every 20-40 seconds
const randomInteraction = () => {
  if (!showMessage.value && Math.random() > 0.8) {
    interactWithPet()
  }
  setTimeout(randomInteraction, 20000 + Math.random() * 20000)
}

onMounted(() => {
  // Start position
  position.value.x = Math.random() * (window.innerWidth - 100)
  position.value.y = Math.random() * (window.innerHeight - 100)
  
  // Initial velocity
  velocity.value.x = (Math.random() - 0.5) * 2
  velocity.value.y = (Math.random() - 0.5) * 2

  // Start animation loop
  const animationLoop = () => {
    movePet()
    requestAnimationFrame(animationLoop)
  }
  animationLoop()

  // Start random interactions
  randomInteraction()

  // Handle window resize
  const handleResize = () => {
    position.value.x = Math.min(position.value.x, window.innerWidth - 64)
    position.value.y = Math.min(position.value.y, window.innerHeight - 64)
  }
  window.addEventListener('resize', handleResize)
})

onUnmounted(() => {
  window.removeEventListener('resize', handleResize)
})
</script>

<style scoped>
.animate-fade-out {
  animation: fadeOut 1s ease-out forwards;
}

@keyframes fadeOut {
  0% {
    opacity: 0.6;
    transform: scale(1);
  }
  100% {
    opacity: 0;
    transform: scale(0);
  }
}

/* Smooth rotation for direction change */
.transition-all {
  transition-property: all;
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
  transition-duration: 1000ms;
}
</style>