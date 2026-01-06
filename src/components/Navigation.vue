<template>
  <nav class="navigation" :class="{ 'scrolled': isScrolled }">
    <div class="nav-container">
      <div class="logo">
        <span class="glitch" data-text="STEEL VENGEANCE">STEEL VENGEANCE</span>
      </div>
      
      <ul class="nav-links">
        <li v-for="item in navItems" :key="item.id">
          <a 
            @click.prevent="handleNavigate(item.id)" 
            :class="{ active: activeSection === item.id }"
            class="nav-link"
          >
            {{ item.label }}
          </a>
        </li>
      </ul>
      
      <button class="mobile-menu-btn" @click="toggleMobile">
        <i :class="mobileOpen ? 'fas fa-times' : 'fas fa-bars'"></i>
      </button>
    </div>
    
    <!-- Mobile menu -->
    <transition name="slide-down">
      <div v-if="mobileOpen" class="mobile-menu">
        <ul>
          <li v-for="item in navItems" :key="item.id">
            <a 
              @click="handleNavigate(item.id)" 
              :class="{ active: activeSection === item.id }"
            >
              {{ item.label }}
            </a>
          </li>
        </ul>
      </div>
    </transition>
  </nav>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const props = defineProps({
  activeSection: String
})

const emit = defineEmits(['navigate'])

const isScrolled = ref(false)
const mobileOpen = ref(false)

const navItems = [
  { id: 'home', label: 'Home' },
  { id: 'tour-dates', label: 'Tour Dates' },
  { id: 'music', label: 'Music' },
  { id: 'merch', label: 'Merch' },
  { id: 'contact', label: 'Contact' }
]

const handleNavigate = (id) => {
  emit('navigate', id)
  mobileOpen.value = false
}

const toggleMobile = () => {
  mobileOpen.value = !mobileOpen.value
}

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
.navigation {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  background: rgba(10, 10, 10, 0.7);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid rgba(255, 0, 51, 0.1);
  transition: all 0.3s ease;
}

.navigation.scrolled {
  background: rgba(10, 10, 10, 0.95);
  border-bottom-color: rgba(255, 0, 51, 0.3);
}

.nav-container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 1.5rem 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  font-size: 1.5rem;
  font-weight: 900;
  letter-spacing: 2px;
  color: #fff;
  text-transform: uppercase;
  font-family: Impact, sans-serif;
}

.nav-links {
  display: flex;
  gap: 3rem;
  list-style: none;
}

.nav-link {
  color: #fff;
  text-decoration: none;
  font-size: 1.1rem;
  font-weight: 600;
  letter-spacing: 1px;
  text-transform: uppercase;
  position: relative;
  cursor: pointer;
  transition: color 0.3s ease;
  padding: 0.5rem 0;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: #ff0033;
  transition: width 0.3s ease;
}

.nav-link:hover,
.nav-link.active {
  color: #ff0033;
}

.nav-link:hover::after,
.nav-link.active::after {
  width: 100%;
}

.mobile-menu-btn {
  display: none;
  background: none;
  border: none;
  color: #fff;
  font-size: 1.5rem;
  cursor: pointer;
  transition: color 0.3s ease;
}

.mobile-menu-btn:hover {
  color: #ff0033;
}

.mobile-menu {
  background: rgba(10, 10, 10, 0.98);
  border-top: 1px solid rgba(255, 0, 51, 0.2);
}

.mobile-menu ul {
  list-style: none;
  padding: 1rem 2rem;
}

.mobile-menu li {
  margin: 0.5rem 0;
}

.mobile-menu a {
  color: #fff;
  text-decoration: none;
  font-size: 1.2rem;
  font-weight: 600;
  text-transform: uppercase;
  display: block;
  padding: 0.75rem;
  transition: all 0.3s ease;
  cursor: pointer;
}

.mobile-menu a:hover,
.mobile-menu a.active {
  color: #ff0033;
  transform: translateX(10px);
}

/* Transitions */
.slide-down-enter-active,
.slide-down-leave-active {
  transition: all 0.3s ease;
}

.slide-down-enter-from,
.slide-down-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}

@media (max-width: 768px) {
  .nav-links {
    display: none;
  }
  
  .mobile-menu-btn {
    display: block;
  }
  
  .logo {
    font-size: 1.2rem;
  }
}
</style>

