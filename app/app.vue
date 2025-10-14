<template>
  <div class="min-h-screen bg-gradient-to-br from-gray-900 via-gray-800 to-gray-900">
    <Navbar />
    <NuxtPage />
    <slot/>
    <FloatingPets/>
    <slot/>
    <CatPet/>
  
    <Footer />
  </div>
</template>

<script setup>

useSeoMeta({
  title: 'Ismaliza - Fullstack Developer',
  description: 'Fullstack Developer specializing in modern web technologies',
  ogImage: '/og-image.png'
})
</script>