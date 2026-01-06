<template>
  <section class="spotify-section">
    <div class="container">
      <div class="spotify-card">
        <div class="spotify-content">
          <div class="spotify-icon">
            <i class="fab fa-spotify"></i>
          </div>
          
          <div class="spotify-info">
            <h2 class="spotify-title">LISTEN ON SPOTIFY</h2>
            <p class="spotify-subtitle">Stream our latest album now</p>
            <div class="player-mock">
              <div class="album-art">
                <img src="https://images.unsplash.com/photo-1614613535308-eb5fbd3d2c17?w=400&h=400&fit=crop" alt="Album">
                <div class="play-overlay">
                  <i class="fas fa-play"></i>
                </div>
              </div>
              
              <div class="player-controls">
                <div class="track-info">
                  <h3 class="track-name">Rise of the Fallen</h3>
                  <p class="track-artist">Steel Vengeance</p>
                </div>
                
                <div class="controls-bar">
                  <button class="control-btn">
                    <i class="fas fa-backward"></i>
                  </button>
                  <button class="control-btn play-btn">
                    <i :class="isPlaying ? 'fas fa-pause' : 'fas fa-play'" @click="togglePlay"></i>
                  </button>
                  <button class="control-btn">
                    <i class="fas fa-forward"></i>
                  </button>
                  <button class="control-btn">
                    <i class="fas fa-random"></i>
                  </button>
                </div>
                
                <div class="progress-bar">
                  <div class="progress-time">{{ currentTime }}</div>
                  <div class="progress-track">
                    <div class="progress-fill" :style="{ width: `${progress}%` }"></div>
                  </div>
                  <div class="progress-time">{{ duration }}</div>
                </div>
              </div>
            </div>
            
            <a href="https://open.spotify.com" target="_blank" class="btn-spotify">
              <i class="fab fa-spotify"></i>
              Open Spotify
            </a>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const isPlaying = ref(false)
const progress = ref(0)
const currentTime = ref('0:00')
const duration = ref('4:23')

let interval = null

const togglePlay = () => {
  isPlaying.value = !isPlaying.value
  
  if (isPlaying.value) {
    interval = setInterval(() => {
      if (progress.value < 100) {
        progress.value += 0.5
        const seconds = Math.floor((progress.value / 100) * 263)
        const mins = Math.floor(seconds / 60)
        const secs = seconds % 60
        currentTime.value = `${mins}:${secs.toString().padStart(2, '0')}`
      } else {
        progress.value = 0
        currentTime.value = '0:00'
        isPlaying.value = false
        clearInterval(interval)
      }
    }, 100)
  } else {
    clearInterval(interval)
  }
}

onUnmounted(() => {
  if (interval) clearInterval(interval)
})
</script>

<style scoped>
.spotify-section {
  padding: 4rem 2rem;
  background: linear-gradient(180deg, #0a0a0a 0%, #0d1117 100%);
  position: relative;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
}

.spotify-card {
  background: linear-gradient(135deg, rgba(30, 215, 96, 0.1) 0%, rgba(26, 26, 26, 0.9) 100%);
  border: 2px solid rgba(30, 215, 96, 0.3);
  border-radius: 20px;
  padding: 3rem;
  position: relative;
  overflow: hidden;
  box-shadow: 0 10px 50px rgba(30, 215, 96, 0.2);
}

.spotify-card::before {
  content: '';
  position: absolute;
  top: -50%;
  right: -50%;
  width: 200%;
  height: 200%;
  background: radial-gradient(circle, rgba(30, 215, 96, 0.1) 0%, transparent 70%);
  animation: rotate 20s linear infinite;
}

@keyframes rotate {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

.spotify-content {
  position: relative;
  z-index: 1;
}

.spotify-icon {
  text-align: center;
  margin-bottom: 2rem;
}

.spotify-icon i {
  font-size: 5rem;
  color: #1DB954;
  filter: drop-shadow(0 0 20px rgba(30, 215, 96, 0.5));
  animation: float 3s ease-in-out infinite;
}

.spotify-title {
  font-size: 3rem;
  font-weight: 900;
  text-align: center;
  margin-bottom: 0.5rem;
  letter-spacing: 3px;
  font-family: Impact, sans-serif;
  background: linear-gradient(90deg, #fff, #1DB954);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.spotify-subtitle {
  text-align: center;
  color: #999;
  font-size: 1.1rem;
  margin-bottom: 3rem;
  letter-spacing: 1px;
}

.player-mock {
  background: rgba(0, 0, 0, 0.5);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 15px;
  padding: 2rem;
  margin-bottom: 2rem;
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 2rem;
  align-items: center;
  backdrop-filter: blur(10px);
}

.album-art {
  position: relative;
  width: 150px;
  height: 150px;
  border-radius: 10px;
  overflow: hidden;
  cursor: pointer;
  transition: transform 0.3s ease;
}

.album-art:hover {
  transform: scale(1.05);
}

.album-art img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.play-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.6);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.album-art:hover .play-overlay {
  opacity: 1;
}

.play-overlay i {
  font-size: 3rem;
  color: #fff;
}

.player-controls {
  flex: 1;
}

.track-info {
  margin-bottom: 1.5rem;
}

.track-name {
  font-size: 1.5rem;
  font-weight: 700;
  margin-bottom: 0.25rem;
}

.track-artist {
  color: #999;
  font-size: 1rem;
}

.controls-bar {
  display: flex;
  gap: 1rem;
  justify-content: center;
  margin-bottom: 1.5rem;
}

.control-btn {
  background: none;
  border: none;
  color: #fff;
  font-size: 1.2rem;
  cursor: pointer;
  transition: all 0.3s ease;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
}

.control-btn:hover {
  color: #1DB954;
  background: rgba(30, 215, 96, 0.1);
}

.play-btn {
  background: #1DB954;
  font-size: 1.5rem;
  width: 50px;
  height: 50px;
}

.play-btn:hover {
  background: #1ed760;
  transform: scale(1.1);
}

.progress-bar {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.progress-time {
  font-size: 0.85rem;
  color: #999;
  min-width: 40px;
}

.progress-track {
  flex: 1;
  height: 6px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 3px;
  overflow: hidden;
  cursor: pointer;
}

.progress-fill {
  height: 100%;
  background: #1DB954;
  transition: width 0.1s linear;
  position: relative;
}

.progress-fill::after {
  content: '';
  position: absolute;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
  width: 12px;
  height: 12px;
  background: #fff;
  border-radius: 50%;
  box-shadow: 0 0 10px rgba(255, 255, 255, 0.5);
}

.btn-spotify {
  display: inline-flex;
  align-items: center;
  gap: 0.75rem;
  padding: 1rem 2.5rem;
  background: #1DB954;
  color: #fff;
  text-decoration: none;
  font-weight: 700;
  font-size: 1.1rem;
  letter-spacing: 1px;
  text-transform: uppercase;
  border-radius: 50px;
  transition: all 0.3s ease;
  margin: 0 auto;
  display: flex;
  width: fit-content;
  box-shadow: 0 5px 20px rgba(30, 215, 96, 0.3);
}

.btn-spotify:hover {
  background: #1ed760;
  transform: translateY(-3px);
  box-shadow: 0 8px 30px rgba(30, 215, 96, 0.5);
}

@media (max-width: 768px) {
  .spotify-title {
    font-size: 2rem;
  }
  
  .player-mock {
    grid-template-columns: 1fr;
    text-align: center;
  }
  
  .album-art {
    margin: 0 auto;
  }
  
  .spotify-card {
    padding: 2rem 1rem;
  }
}
</style>

