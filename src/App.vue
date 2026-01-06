<template>
  <div class="app">
    <!-- Noise and scanline effects -->
    <div class="noise"></div>
    <div class="scanline"></div>
    
    <!-- Navigation -->
    <Navigation :active-section="activeSection" @navigate="scrollToSection" />
    
    <!-- Main content -->
    <main class="main-content">
      <Hero id="home" />
      <TourDates id="tour-dates" />
      <SpotifyPlayer />
      <Music id="music" />
      <Merch id="merch" />
      <Contact id="contact" />
    </main>
    
    <!-- Footer -->
    <footer class="bg-metal-dark border-t border-metal-red/20 py-8">
      <div class="container mx-auto px-4 text-center">
        <div class="flex justify-center space-x-6 mb-4">
          <a href="https://spotify.com" target="_blank" class="text-white hover:text-metal-red transition-colors">
            <i class="fab fa-spotify text-2xl"></i>
          </a>
          <a href="https://youtube.com" target="_blank" class="text-white hover:text-metal-red transition-colors">
            <i class="fab fa-youtube text-2xl"></i>
          </a>
          <a href="https://instagram.com" target="_blank" class="text-white hover:text-metal-red transition-colors">
            <i class="fab fa-instagram text-2xl"></i>
          </a>
          <a href="https://facebook.com" target="_blank" class="text-white hover:text-metal-red transition-colors">
            <i class="fab fa-facebook text-2xl"></i>
          </a>
        </div>
        <p class="text-gray-400 text-sm">© 2026 STEEL VENGEANCE. All rights reserved.</p>
        <p class="text-gray-500 text-xs mt-2">
          Built with <span class="text-metal-red">♥</span> by 
          <a href="https://github.com/onurceyhan" target="_blank" class="text-metal-red hover:underline">@onurceyhan</a>
        </p>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import Navigation from './components/Navigation.vue'
import Hero from './components/Hero.vue'
import TourDates from './components/TourDates.vue'
import SpotifyPlayer from './components/SpotifyPlayer.vue'
import Music from './components/Music.vue'
import Merch from './components/Merch.vue'
import Contact from './components/Contact.vue'

const activeSection = ref('home')

const scrollToSection = (sectionId) => {
  const element = document.getElementById(sectionId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}

onMounted(() => {
  // Observe sections for active navigation
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          activeSection.value = entry.target.id
        }
      })
    },
    { threshold: 0.3 }
  )

  document.querySelectorAll('section').forEach((section) => {
    observer.observe(section)
  })
})
</script>

<style scoped>
.app {
  min-height: 100vh;
  background: linear-gradient(180deg, #0a0a0a 0%, #1a0a0a 100%);
}

.main-content {
  position: relative;
  z-index: 1;
}
</style>

