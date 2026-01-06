<template>
  <section id="tour-dates" class="tour-section">
    <div class="container">
      <h2 class="section-title glitch" data-text="TOUR DATES">TOUR DATES</h2>
      <p class="section-subtitle">Catch us live on the road</p>
      
      <div class="tour-grid">
        <div 
          v-for="(show, index) in shows" 
          :key="index" 
          class="tour-card"
          :style="{ animationDelay: `${index * 0.1}s` }"
        >
          <div class="tour-date">
            <div class="date-day">{{ show.day }}</div>
            <div class="date-month">{{ show.month }}</div>
          </div>
          
          <div class="tour-info">
            <h3 class="tour-venue">{{ show.venue }}</h3>
            <p class="tour-location">
              <i class="fas fa-map-marker-alt"></i>
              {{ show.city }}, {{ show.country }}
            </p>
            <p class="tour-time">
              <i class="fas fa-clock"></i>
              {{ show.time }}
            </p>
          </div>
          
          <div class="tour-action">
            <button class="btn-tickets" :class="{ 'sold-out': show.soldOut }">
              {{ show.soldOut ? 'SOLD OUT' : 'TICKETS' }}
            </button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const shows = ref([
  { day: '15', month: 'FEB', venue: 'Wembley Arena', city: 'London', country: 'UK', time: '8:00 PM', soldOut: false },
  { day: '18', month: 'FEB', venue: 'Olympiahalle', city: 'Munich', country: 'Germany', time: '7:30 PM', soldOut: false },
  { day: '22', month: 'FEB', venue: 'Accor Arena', city: 'Paris', country: 'France', time: '9:00 PM', soldOut: true },
  { day: '25', month: 'FEB', venue: 'Ziggo Dome', city: 'Amsterdam', country: 'Netherlands', time: '8:00 PM', soldOut: false },
  { day: '28', month: 'FEB', venue: 'Barclays Center', city: 'New York', country: 'USA', time: '7:00 PM', soldOut: false },
  { day: '03', month: 'MAR', venue: 'Madison Square Garden', city: 'New York', country: 'USA', time: '8:00 PM', soldOut: true },
  { day: '07', month: 'MAR', venue: 'The Forum', city: 'Los Angeles', country: 'USA', time: '9:00 PM', soldOut: false },
  { day: '10', month: 'MAR', venue: 'Budokan', city: 'Tokyo', country: 'Japan', time: '7:00 PM', soldOut: false },
  { day: '15', month: 'MAR', venue: 'Rod Laver Arena', city: 'Melbourne', country: 'Australia', time: '8:30 PM', soldOut: false },
])
</script>

<style scoped>
.tour-section {
  min-height: 100vh;
  padding: 6rem 2rem;
  background: linear-gradient(180deg, #0a0a0a 0%, #1a0a0a 50%, #0a0a0a 100%);
  position: relative;
}

.tour-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: url('data:image/svg+xml,<svg width="100" height="100" xmlns="http://www.w3.org/2000/svg"><defs><pattern id="grid" width="100" height="100" patternUnits="userSpaceOnUse"><path d="M 100 0 L 0 0 0 100" fill="none" stroke="rgba(255,0,51,0.05)" stroke-width="1"/></pattern></defs><rect width="100" height="100" fill="url(%23grid)"/></svg>');
  pointer-events: none;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  position: relative;
  z-index: 1;
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

.tour-grid {
  display: grid;
  gap: 1.5rem;
}

.tour-card {
  background: rgba(26, 26, 26, 0.8);
  border: 1px solid rgba(255, 0, 51, 0.2);
  padding: 1.5rem;
  display: grid;
  grid-template-columns: auto 1fr auto;
  gap: 2rem;
  align-items: center;
  transition: all 0.3s ease;
  animation: slide-up 0.6s ease-out forwards;
  opacity: 0;
  position: relative;
  overflow: hidden;
}

.tour-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 0, 51, 0.1), transparent);
  transition: left 0.5s ease;
}

.tour-card:hover {
  border-color: #ff0033;
  transform: translateX(10px);
  box-shadow: 
    -5px 0 0 #ff0033,
    0 0 30px rgba(255, 0, 51, 0.3);
}

.tour-card:hover::before {
  left: 100%;
}

.tour-date {
  text-align: center;
  padding: 1rem 1.5rem;
  background: rgba(255, 0, 51, 0.1);
  border: 2px solid #ff0033;
  min-width: 80px;
}

.date-day {
  font-size: 2rem;
  font-weight: 900;
  color: #ff0033;
  line-height: 1;
}

.date-month {
  font-size: 1rem;
  font-weight: 700;
  color: #fff;
  margin-top: 0.25rem;
  letter-spacing: 2px;
}

.tour-info {
  flex: 1;
}

.tour-venue {
  font-size: 1.5rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
  color: #fff;
}

.tour-location,
.tour-time {
  color: #999;
  font-size: 0.95rem;
  margin: 0.25rem 0;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.tour-location i,
.tour-time i {
  color: #ff0033;
  width: 16px;
}

.btn-tickets {
  padding: 0.75rem 2rem;
  background: #ff0033;
  color: #fff;
  border: none;
  font-weight: 700;
  font-size: 1rem;
  letter-spacing: 1px;
  cursor: pointer;
  transition: all 0.3s ease;
  text-transform: uppercase;
  position: relative;
  overflow: hidden;
}

.btn-tickets::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  width: 0;
  height: 0;
  background: rgba(255, 255, 255, 0.2);
  border-radius: 50%;
  transform: translate(-50%, -50%);
  transition: width 0.5s, height 0.5s;
}

.btn-tickets:hover::before {
  width: 300px;
  height: 300px;
}

.btn-tickets:hover {
  transform: scale(1.05);
  box-shadow: 0 0 20px rgba(255, 0, 51, 0.5);
}

.btn-tickets.sold-out {
  background: #333;
  cursor: not-allowed;
  opacity: 0.6;
}

.btn-tickets.sold-out:hover {
  transform: none;
  box-shadow: none;
}

@keyframes slide-up {
  to {
    opacity: 1;
    transform: translateY(0);
  }
  from {
    opacity: 0;
    transform: translateY(20px);
  }
}

@media (max-width: 768px) {
  .section-title {
    font-size: 2.5rem;
  }
  
  .tour-card {
    grid-template-columns: 1fr;
    text-align: center;
    gap: 1rem;
  }
  
  .tour-date {
    margin: 0 auto;
  }
  
  .tour-location,
  .tour-time {
    justify-content: center;
  }
  
  .tour-card:hover {
    transform: translateY(-5px);
  }
}
</style>

