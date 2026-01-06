<template>
  <section id="home" class="hero">
    <div class="hero-content">
      <div class="hero-left">
        <div class="hero-image-container">
          <div class="glitch-image">
            <div class="glitch-layer layer-1"></div>
            <div class="glitch-layer layer-2"></div>
            <div class="glitch-layer layer-3"></div>
            <img 
              src="https://images.unsplash.com/photo-1498038432885-c6f3f1b912ee?w=800&h=800&fit=crop" 
              alt="Band" 
              class="hero-img"
            />
          </div>
        </div>
      </div>
      
      <div class="hero-right">
        <div class="hero-text">
          <h1 class="glitch glitch-large" data-text="STEEL VENGEANCE">
            STEEL VENGEANCE
          </h1>
          <p class="hero-subtitle animate-slide-up">
            THE STORM IS COMING
          </p>
          <div class="hero-buttons animate-slide-up">
            <button @click="$emit('navigate', 'tour-dates')" class="btn btn-primary">
              <i class="fas fa-ticket-alt"></i> Tour Dates
            </button>
            <button @click="scrollToMusic" class="btn btn-secondary">
              <i class="fas fa-play"></i> Listen Now
            </button>
          </div>
        </div>
        
        <div class="hero-stats">
          <div class="stat" v-for="(stat, index) in stats" :key="index">
            <div class="stat-value">{{ stat.value }}</div>
            <div class="stat-label">{{ stat.label }}</div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="scroll-indicator">
      <i class="fas fa-chevron-down"></i>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

defineEmits(['navigate'])

const stats = ref([
  { value: '500K+', label: 'Monthly Listeners' },
  { value: '50+', label: 'Shows This Year' },
  { value: '5', label: 'Studio Albums' }
])

const scrollToMusic = () => {
  document.getElementById('music')?.scrollIntoView({ behavior: 'smooth' })
}
</script>

<style scoped>
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 6rem 2rem 2rem;
  position: relative;
  overflow: hidden;
}

.hero::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: 
    radial-gradient(circle at 20% 50%, rgba(255, 0, 51, 0.1) 0%, transparent 50%),
    radial-gradient(circle at 80% 50%, rgba(255, 0, 51, 0.05) 0%, transparent 50%);
  pointer-events: none;
}

.hero-content {
  max-width: 1400px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
  position: relative;
  z-index: 1;
}

.hero-image-container {
  position: relative;
}

.glitch-image {
  position: relative;
  width: 100%;
  max-width: 500px;
  aspect-ratio: 1;
  overflow: hidden;
  border: 2px solid #ff0033;
  box-shadow: 
    0 0 20px rgba(255, 0, 51, 0.3),
    inset 0 0 20px rgba(255, 0, 51, 0.1);
}

.hero-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: grayscale(40%) contrast(1.2);
  transition: transform 0.3s ease;
}

.glitch-image:hover .hero-img {
  transform: scale(1.05);
}

.glitch-layer {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: url('https://images.unsplash.com/photo-1498038432885-c6f3f1b912ee?w=800&h=800&fit=crop');
  background-size: cover;
  opacity: 0;
  mix-blend-mode: screen;
}

.layer-1 {
  animation: glitch-1 3s infinite;
}

.layer-2 {
  animation: glitch-2 2s infinite;
}

.layer-3 {
  animation: glitch-3 2.5s infinite;
}

@keyframes glitch-1 {
  0%, 90%, 100% { opacity: 0; transform: translate(0); }
  91%, 93% { opacity: 0.7; transform: translate(-2px, 2px); }
}

@keyframes glitch-2 {
  0%, 80%, 100% { opacity: 0; transform: translate(0); }
  81%, 84% { opacity: 0.5; transform: translate(2px, -2px); }
}

@keyframes glitch-3 {
  0%, 85%, 100% { opacity: 0; transform: translate(0); }
  86%, 88% { opacity: 0.6; transform: translate(-3px, -1px); }
}

.hero-text {
  margin-bottom: 3rem;
}

.glitch-large {
  font-size: 4rem;
  font-weight: 900;
  margin-bottom: 1rem;
  line-height: 1;
  letter-spacing: 3px;
  text-transform: uppercase;
  font-family: Impact, sans-serif;
}

.hero-subtitle {
  font-size: 1.5rem;
  color: #ff0033;
  font-weight: 700;
  letter-spacing: 4px;
  margin-bottom: 2rem;
  animation: pulse-red 2s infinite;
}

.hero-buttons {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
}

.btn {
  padding: 1rem 2rem;
  font-size: 1rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1px;
  border: none;
  cursor: pointer;
  transition: all 0.3s ease;
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
}

.btn-primary {
  background: #ff0033;
  color: #fff;
  box-shadow: 0 0 20px rgba(255, 0, 51, 0.5);
}

.btn-primary:hover {
  background: #cc0029;
  transform: translateY(-2px);
  box-shadow: 0 5px 30px rgba(255, 0, 51, 0.7);
}

.btn-secondary {
  background: transparent;
  color: #fff;
  border: 2px solid #fff;
}

.btn-secondary:hover {
  background: #fff;
  color: #0a0a0a;
  transform: translateY(-2px);
}

.hero-stats {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
  padding-top: 2rem;
  border-top: 1px solid rgba(255, 0, 51, 0.3);
}

.stat {
  text-align: center;
}

.stat-value {
  font-size: 2rem;
  font-weight: 900;
  color: #ff0033;
  margin-bottom: 0.5rem;
}

.stat-label {
  font-size: 0.9rem;
  color: #999;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.scroll-indicator {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  font-size: 2rem;
  color: #ff0033;
  animation: float 3s ease-in-out infinite;
  cursor: pointer;
}

.animate-slide-up {
  animation: slide-up 0.8s ease-out;
}

@keyframes slide-up {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@media (max-width: 968px) {
  .hero-content {
    grid-template-columns: 1fr;
    text-align: center;
  }
  
  .glitch-image {
    margin: 0 auto;
  }
  
  .hero-buttons {
    justify-content: center;
  }
  
  .glitch-large {
    font-size: 3rem;
  }
}

@media (max-width: 640px) {
  .glitch-large {
    font-size: 2rem;
  }
  
  .hero-subtitle {
    font-size: 1.2rem;
  }
  
  .hero-stats {
    grid-template-columns: 1fr;
  }
}
</style>

