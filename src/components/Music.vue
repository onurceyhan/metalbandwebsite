<template>
  <section id="music" class="music-section">
    <div class="container">
      <h2 class="section-title glitch" data-text="MUSIC">MUSIC</h2>
      <p class="section-subtitle">Explore our discography</p>
      
      <div class="albums-grid">
        <div 
          v-for="(album, index) in albums" 
          :key="index" 
          class="album-card"
          :style="{ animationDelay: `${index * 0.15}s` }"
        >
          <div class="album-cover">
            <img :src="album.cover" :alt="album.title" />
            <div class="album-overlay">
              <button class="play-album">
                <i class="fas fa-play"></i>
              </button>
              <div class="album-actions">
                <a :href="album.spotify" target="_blank" class="action-btn">
                  <i class="fab fa-spotify"></i>
                </a>
                <a :href="album.apple" target="_blank" class="action-btn">
                  <i class="fab fa-apple"></i>
                </a>
                <a :href="album.youtube" target="_blank" class="action-btn">
                  <i class="fab fa-youtube"></i>
                </a>
              </div>
            </div>
          </div>
          
          <div class="album-info">
            <h3 class="album-title">{{ album.title }}</h3>
            <p class="album-year">{{ album.year }}</p>
            <div class="album-stats">
              <span><i class="fas fa-music"></i> {{ album.tracks }} tracks</span>
            </div>
          </div>
        </div>
      </div>
      
      <div class="music-cta">
        <h3 class="cta-title">Stream Our Music Everywhere</h3>
        <div class="platform-links">
          <a href="https://spotify.com" target="_blank" class="platform-btn spotify">
            <i class="fab fa-spotify"></i>
            <span>Spotify</span>
          </a>
          <a href="https://music.apple.com" target="_blank" class="platform-btn apple">
            <i class="fab fa-apple"></i>
            <span>Apple Music</span>
          </a>
          <a href="https://youtube.com" target="_blank" class="platform-btn youtube">
            <i class="fab fa-youtube"></i>
            <span>YouTube</span>
          </a>
          <a href="https://deezer.com" target="_blank" class="platform-btn deezer">
            <i class="fas fa-compact-disc"></i>
            <span>Deezer</span>
          </a>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const albums = ref([
  {
    title: 'Eternal Darkness',
    year: '2024',
    tracks: 12,
    cover: 'https://images.unsplash.com/photo-1614613535308-eb5fbd3d2c17?w=500&h=500&fit=crop',
    spotify: 'https://spotify.com',
    apple: 'https://music.apple.com',
    youtube: 'https://youtube.com'
  },
  {
    title: 'Rise of the Fallen',
    year: '2022',
    tracks: 10,
    cover: 'https://images.unsplash.com/photo-1619983081563-430f63602796?w=500&h=500&fit=crop',
    spotify: 'https://spotify.com',
    apple: 'https://music.apple.com',
    youtube: 'https://youtube.com'
  },
  {
    title: 'Blood & Steel',
    year: '2020',
    tracks: 11,
    cover: 'https://images.unsplash.com/photo-1601042879364-f3947d3f9c16?w=500&h=500&fit=crop',
    spotify: 'https://spotify.com',
    apple: 'https://music.apple.com',
    youtube: 'https://youtube.com'
  },
  {
    title: 'Vengeance',
    year: '2018',
    tracks: 9,
    cover: 'https://images.unsplash.com/photo-1470225620780-dba8ba36b745?w=500&h=500&fit=crop',
    spotify: 'https://spotify.com',
    apple: 'https://music.apple.com',
    youtube: 'https://youtube.com'
  }
])
</script>

<style scoped>
.music-section {
  min-height: 100vh;
  padding: 6rem 2rem;
  background: linear-gradient(180deg, #0a0a0a 0%, #0d0d0d 100%);
  position: relative;
}

.container {
  max-width: 1400px;
  margin: 0 auto;
}

.section-title {
  font-size: 4rem;
  font-weight: 900;
  text-align: center;
  margin-bottom: 1rem;
  letter-spacing: 4px;
  font-family: Impact, sans-serif;
}

.section-subtitle {
  text-align: center;
  font-size: 1.2rem;
  color: #999;
  margin-bottom: 4rem;
  letter-spacing: 2px;
  text-transform: uppercase;
}

.albums-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 2rem;
  margin-bottom: 4rem;
}

.album-card {
  background: rgba(26, 26, 26, 0.5);
  border: 1px solid rgba(255, 0, 51, 0.2);
  transition: all 0.3s ease;
  animation: fade-in 0.6s ease-out forwards;
  opacity: 0;
  position: relative;
  overflow: hidden;
}

.album-card::before {
  content: '';
  position: absolute;
  top: -100%;
  left: 0;
  right: 0;
  height: 100%;
  background: linear-gradient(180deg, rgba(255, 0, 51, 0.2), transparent);
  transition: top 0.5s ease;
}

.album-card:hover {
  border-color: #ff0033;
  transform: translateY(-10px);
  box-shadow: 0 10px 40px rgba(255, 0, 51, 0.3);
}

.album-card:hover::before {
  top: 0;
}

.album-cover {
  position: relative;
  aspect-ratio: 1;
  overflow: hidden;
}

.album-cover img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.album-card:hover .album-cover img {
  transform: scale(1.1);
}

.album-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s ease;
  gap: 1.5rem;
}

.album-card:hover .album-overlay {
  opacity: 1;
}

.play-album {
  width: 70px;
  height: 70px;
  border-radius: 50%;
  background: #ff0033;
  border: none;
  color: #fff;
  font-size: 1.8rem;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s ease;
  box-shadow: 0 0 30px rgba(255, 0, 51, 0.5);
}

.play-album:hover {
  transform: scale(1.1);
  box-shadow: 0 0 50px rgba(255, 0, 51, 0.8);
}

.album-actions {
  display: flex;
  gap: 1rem;
}

.action-btn {
  width: 45px;
  height: 45px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.1);
  border: 1px solid rgba(255, 255, 255, 0.3);
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  text-decoration: none;
  font-size: 1.2rem;
  transition: all 0.3s ease;
}

.action-btn:hover {
  background: #fff;
  color: #0a0a0a;
  transform: translateY(-3px);
}

.album-info {
  padding: 1.5rem;
}

.album-title {
  font-size: 1.3rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
  color: #fff;
}

.album-year {
  color: #ff0033;
  font-weight: 600;
  margin-bottom: 0.75rem;
}

.album-stats {
  color: #999;
  font-size: 0.9rem;
}

.album-stats i {
  color: #ff0033;
  margin-right: 0.25rem;
}

.music-cta {
  text-align: center;
  padding: 4rem 2rem;
  background: rgba(255, 0, 51, 0.05);
  border: 2px solid rgba(255, 0, 51, 0.2);
  border-radius: 20px;
}

.cta-title {
  font-size: 2rem;
  font-weight: 700;
  margin-bottom: 2rem;
  letter-spacing: 2px;
}

.platform-links {
  display: flex;
  gap: 1.5rem;
  justify-content: center;
  flex-wrap: wrap;
}

.platform-btn {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 1rem 2rem;
  background: rgba(255, 255, 255, 0.05);
  border: 2px solid rgba(255, 255, 255, 0.2);
  color: #fff;
  text-decoration: none;
  font-weight: 600;
  font-size: 1rem;
  border-radius: 50px;
  transition: all 0.3s ease;
}

.platform-btn i {
  font-size: 1.5rem;
}

.platform-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 5px 20px rgba(255, 255, 255, 0.2);
}

.platform-btn.spotify:hover {
  background: #1DB954;
  border-color: #1DB954;
  box-shadow: 0 5px 20px rgba(30, 215, 96, 0.4);
}

.platform-btn.apple:hover {
  background: linear-gradient(135deg, #FA243C, #FF6D5A);
  border-color: #FA243C;
  box-shadow: 0 5px 20px rgba(250, 36, 60, 0.4);
}

.platform-btn.youtube:hover {
  background: #FF0000;
  border-color: #FF0000;
  box-shadow: 0 5px 20px rgba(255, 0, 0, 0.4);
}

.platform-btn.deezer:hover {
  background: #FF0092;
  border-color: #FF0092;
  box-shadow: 0 5px 20px rgba(255, 0, 146, 0.4);
}

@keyframes fade-in {
  to {
    opacity: 1;
  }
}

@media (max-width: 768px) {
  .section-title {
    font-size: 2.5rem;
  }
  
  .albums-grid {
    grid-template-columns: 1fr;
    max-width: 400px;
    margin: 0 auto 4rem;
  }
  
  .platform-links {
    flex-direction: column;
    align-items: center;
  }
  
  .platform-btn {
    width: 100%;
    max-width: 300px;
    justify-content: center;
  }
}
</style>

