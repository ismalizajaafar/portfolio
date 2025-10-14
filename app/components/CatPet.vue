<template>
  <div 
    ref="petContainer"
    class="fixed z-40 cursor-pointer transition-all duration-1000 ease-linear pixelated"
    :style="{
      left: position.x + 'px',
      top: position.y + 'px',
      transform: `scale(${isHovered ? 1.5 : 1}) scaleX(${velocity.x > 0 ? 1 : -1})`
    }"
    @mouseenter="isHovered = true"
    @mouseleave="isHovered = false"
    @click="interactWithPet"
  >
    <!-- Pixel Calico Cat -->
    <div class="relative pixel-art">
      <!-- Body -->
      <div class="w-16 h-12 bg-white border-2 border-gray-800 relative pixel-grid">
        <!-- Calico patches -->
        <div class="absolute top-0 left-0 w-8 h-6 bg-orange-500 border-r-2 border-b-2 border-gray-800"></div>
        <div class="absolute top-0 right-0 w-6 h-5 bg-black border-l-2 border-b-2 border-gray-800"></div>
        <div class="absolute bottom-0 left-4 w-4 h-3 bg-black border-t-2 border-r-2 border-l-2 border-gray-800"></div>
      </div>
      
      <!-- Head -->
      <div class="absolute -top-5 left-1/2 transform -translate-x-1/2 w-12 h-12 bg-white border-2 border-gray-800 pixel-grid">
        <!-- Calico face patches -->
        <div class="absolute top-0 left-0 w-6 h-6 bg-orange-500 border-r-2 border-b-2 border-gray-800"></div>
        <div class="absolute top-0 right-0 w-5 h-5 bg-black border-l-2 border-b-2 border-gray-800"></div>
        
        <!-- Ears -->
        <div class="absolute -top-2 left-1 w-4 h-4 bg-orange-500 border-2 border-gray-800 rotate-45 transform origin-bottom-right pixel-ear"></div>
        <div class="absolute -top-2 right-1 w-4 h-4 bg-black border-2 border-gray-800 -rotate-45 transform origin-bottom-left pixel-ear"></div>
        
        <!-- Eyes -->
        <div class="absolute top-3 left-2 w-2 h-2 bg-green-400 border border-gray-800"></div>
        <div class="absolute top-3 right-2 w-2 h-2 bg-green-400 border border-gray-800"></div>
        
        <!-- Pupils -->
        <div class="absolute top-3 left-2 w-1 h-1 bg-gray-800" :style="pupilStyle"></div>
        <div class="absolute top-3 right-2 w-1 h-1 bg-gray-800" :style="pupilStyle"></div>
        
        <!-- Nose -->
        <div class="absolute bottom-3 left-1/2 transform -translate-x-1/2 w-2 h-1 bg-pink-400 border border-gray-800"></div>
        
        <!-- Mouth -->
        <div class="absolute bottom-2 left-1/2 transform -translate-x-1/2 w-2 h-0.5 bg-gray-800"></div>
        
        <!-- Whiskers - Left -->
        <div class="absolute bottom-2 left-0 w-2 h-0.5 bg-gray-600 transform -rotate-12"></div>
        <div class="absolute bottom-3 left-0 w-2 h-0.5 bg-gray-600 transform -rotate-6"></div>
        
        <!-- Whiskers - Right -->
        <div class="absolute bottom-2 right-0 w-2 h-0.5 bg-gray-600 transform rotate-12"></div>
        <div class="absolute bottom-3 right-0 w-2 h-0.5 bg-gray-600 transform rotate-6"></div>
      </div>

      <!-- Tail -->
      <div class="absolute -right-4 top-1 w-6 h-2 bg-gradient-to-r from-orange-500 to-black border-2 border-gray-800 transform rotate-12 pixel-tail"></div>
      
      <!-- Legs -->
      <div class="absolute -bottom-1 left-2 w-3 h-2 bg-white border-2 border-t-0 border-gray-800"></div>
      <div class="absolute -bottom-1 right-2 w-3 h-2 bg-white border-2 border-t-0 border-gray-800"></div>

      <!-- Pixel Grid Overlay (visual guide) -->
      <div class="absolute inset-0 pointer-events-none opacity-10 pixel-grid-overlay"></div>
    </div>

    <!-- Speech Bubble -->
    <div 
      v-if="showMessage"
      class="absolute -top-20 left-1/2 transform -translate-x-1/2 bg-white border-2 border-gray-800 px-2 py-1 text-xs font-mono text-gray-800 whitespace-nowrap pixel-bubble"
    >
      {{ currentMessage }}
      <div class="absolute bottom-0 left-1/2 transform -translate-x-1/2 translate-y-1 w-2 h-2 bg-white border-b-2 border-r-2 border-gray-800 rotate-45"></div>
    </div>

    <!-- Pixel Trail Effect -->
    <div 
      v-for="(trail, index) in trails"
      :key="index"
      class="absolute w-1 h-1 bg-orange-400 border border-gray-800 opacity-0 animate-pixel-fade"
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
  'MEOW! 🐱',
  '> CODE GOOD',
  'PLAY TIME!',
  'Zzz... 💤',
  'BUG HUNT!',
  'PIXEL PURRFECT',
  'CAT.EXE RUNNING',
  '404 SLEEP NOT FOUND',
  'COMPILE SUCCESS!',
  'HELLO WORLD!'
]

const pupilStyle = computed(() => {
  const angle = Math.atan2(velocity.value.y, velocity.value.x)
  const offsetX = Math.cos(angle) * 0.5
  const offsetY = Math.sin(angle) * 0.5
  return {
    transform: `translate(${offsetX}px, ${offsetY}px)`
  }
})

const movePet = () => {
  if (isHovered.value) return

  const newX = position.value.x + velocity.value.x
  const newY = position.value.y + velocity.value.y

  // Boundary checking - pixel movement (snap to grid for retro feel)
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

  // Snap to 2px grid for pixel-perfect movement
  position.value.x = Math.round(Math.max(0, Math.min(newX, maxX)) / 2) * 2
  position.value.y = Math.round(Math.max(0, Math.min(newY, maxY)) / 2) * 2

  // Occasionally change direction
  if (Math.random() < 0.02) {
    velocity.value.x = (Math.round(Math.random() * 4) - 2) // -2, -1, 0, 1, 2
    velocity.value.y = (Math.round(Math.random() * 4) - 2)
    velocity.value.x = velocity.value.x === 0 ? 1 : velocity.value.x
    velocity.value.y = velocity.value.y === 0 ? 1 : velocity.value.y
    addTrail()
  }

  // Add trail occasionally
  if (Math.random() < 0.4) {
    addTrail()
  }
}

const addTrail = () => {
  trails.value.push({
    x: (Math.round(Math.random() * 8) - 4) * 2, // Snap to grid
    y: (Math.round(Math.random() * 8) - 4) * 2,
    id: Date.now() + Math.random()
  })

  // Limit trails
  if (trails.value.length > 8) {
    trails.value.shift()
  }
}

const interactWithPet = () => {
  // Change direction on click (pixel grid movement)
  velocity.value.x = (Math.round(Math.random() * 6) - 3)
  velocity.value.y = (Math.round(Math.random() * 6) - 3)
  velocity.value.x = velocity.value.x === 0 ? 2 : velocity.value.x
  velocity.value.y = velocity.value.y === 0 ? 2 : velocity.value.y
  
  // Show random message
  showMessage.value = true
  currentMessage.value = messages[Math.floor(Math.random() * messages.length)]
  
  // Add multiple pixel trails
  for (let i = 0; i < 6; i++) {
    setTimeout(() => addTrail(), i * 80)
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
  // Start position (snap to grid)
  position.value.x = Math.round(Math.random() * (window.innerWidth - 100) / 2) * 2
  position.value.y = Math.round(Math.random() * (window.innerHeight - 100) / 2) * 2
  
  // Initial velocity (pixel grid movement)
  velocity.value.x = (Math.round(Math.random() * 4) - 2) || 1
  velocity.value.y = (Math.round(Math.random() * 4) - 2) || 1

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
.pixelated {
  image-rendering: pixelated;
  image-rendering: -moz-crisp-edges;
  image-rendering: crisp-edges;
}

.pixel-art * {
  image-rendering: pixelated;
  image-rendering: -moz-crisp-edges;
  image-rendering: crisp-edges;
}

.pixel-grid {
  box-shadow: 2px 2px 0px rgba(0, 0, 0, 0.3);
}

.pixel-ear {
  clip-path: polygon(0% 100%, 100% 100%, 100% 0%);
}

.pixel-tail {
  clip-path: polygon(0% 50%, 100% 0%, 100% 100%);
}

.pixel-bubble {
  box-shadow: 2px 2px 0px rgba(0, 0, 0, 0.3);
  font-family: 'Courier New', monospace;
  font-weight: bold;
}

.pixel-grid-overlay {
  background-image: 
    linear-gradient(rgba(0, 0, 0, 0.1) 1px, transparent 1px),
    linear-gradient(90deg, rgba(0, 0, 0, 0.1) 1px, transparent 1px);
  background-size: 4px 4px;
}

.animate-pixel-fade {
  animation: pixelFade 0.8s steps(4) forwards;
}

@keyframes pixelFade {
  0% {
    opacity: 0.8;
    transform: scale(1);
  }
  50% {
    opacity: 0.4;
    transform: scale(0.8);
  }
  100% {
    opacity: 0;
    transform: scale(0.5);
  }
}

/* Ensure crisp pixel borders */
.border-gray-800 {
  border-color: #1f2937 !important;
}
</style>