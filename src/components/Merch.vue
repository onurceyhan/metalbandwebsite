<template>
  <section id="merch" class="merch-section">
    <div class="container">
      <h2 class="section-title glitch" data-text="MERCH">MERCH</h2>
      <p class="section-subtitle">Official band merchandise</p>
      
      <div class="merch-grid">
        <div 
          v-for="(item, index) in merchItems" 
          :key="index" 
          class="merch-card"
          :style="{ animationDelay: `${index * 0.1}s` }"
        >
          <div class="merch-image">
            <img :src="item.image" :alt="item.name" />
            <div class="merch-badge" v-if="item.badge">{{ item.badge }}</div>
            <div class="merch-overlay">
              <button class="quick-view">
                <i class="fas fa-search-plus"></i>
                Quick View
              </button>
            </div>
          </div>
          
          <div class="merch-info">
            <h3 class="merch-name">{{ item.name }}</h3>
            <p class="merch-category">{{ item.category }}</p>
            <div class="merch-footer">
              <span class="merch-price">${{ item.price }}</span>
              <button class="btn-add-cart">
                <i class="fas fa-shopping-cart"></i>
                Add to Cart
              </button>
            </div>
          </div>
        </div>
      </div>
      
      <div class="merch-cta">
        <h3 class="cta-text">
          <i class="fas fa-shipping-fast"></i>
          Free worldwide shipping on orders over $50
        </h3>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const merchItems = ref([
  {
    name: 'Eternal Darkness T-Shirt',
    category: 'Apparel',
    price: 29.99,
    image: 'https://images.unsplash.com/photo-1583743814966-8936f5b7be1a?w=500&h=500&fit=crop',
    badge: 'NEW'
  },
  {
    name: 'Blood & Steel Hoodie',
    category: 'Apparel',
    price: 59.99,
    image: 'https://images.unsplash.com/photo-1556821840-3a63f95609a7?w=500&h=500&fit=crop',
    badge: 'BESTSELLER'
  },
  {
    name: 'Logo Snapback',
    category: 'Accessories',
    price: 24.99,
    image: 'https://images.unsplash.com/photo-1588850561407-ed78c282e89b?w=500&h=500&fit=crop',
    badge: null
  },
  {
    name: 'Vengeance Poster',
    category: 'Collectibles',
    price: 19.99,
    image: 'https://images.unsplash.com/photo-1611162617213-7d7a39e9b1d7?w=500&h=500&fit=crop',
    badge: null
  },
  {
    name: 'Limited Edition Vinyl',
    category: 'Music',
    price: 39.99,
    image: 'https://images.unsplash.com/photo-1619983081563-430f63602796?w=500&h=500&fit=crop',
    badge: 'LIMITED'
  },
  {
    name: 'Band Logo Patch',
    category: 'Accessories',
    price: 9.99,
    image: 'https://images.unsplash.com/photo-1602491453631-e2a5ad90a131?w=500&h=500&fit=crop',
    badge: null
  }
])
</script>

<style scoped>
.merch-section {
  min-height: 100vh;
  padding: 6rem 2rem;
  background: linear-gradient(180deg, #0d0d0d 0%, #0a0a0a 100%);
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

.merch-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 2rem;
  margin-bottom: 4rem;
}

.merch-card {
  background: rgba(26, 26, 26, 0.6);
  border: 1px solid rgba(255, 0, 51, 0.2);
  transition: all 0.3s ease;
  animation: slide-up 0.6s ease-out forwards;
  opacity: 0;
  overflow: hidden;
}

.merch-card:hover {
  border-color: #ff0033;
  transform: translateY(-10px);
  box-shadow: 0 10px 40px rgba(255, 0, 51, 0.3);
}

.merch-image {
  position: relative;
  aspect-ratio: 1;
  overflow: hidden;
}

.merch-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.merch-card:hover .merch-image img {
  transform: scale(1.15);
}

.merch-badge {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: #ff0033;
  color: #fff;
  padding: 0.5rem 1rem;
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 1px;
  text-transform: uppercase;
  z-index: 2;
  box-shadow: 0 0 20px rgba(255, 0, 51, 0.5);
}

.merch-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.85);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.merch-card:hover .merch-overlay {
  opacity: 1;
}

.quick-view {
  padding: 1rem 2rem;
  background: transparent;
  border: 2px solid #fff;
  color: #fff;
  font-weight: 700;
  font-size: 1rem;
  text-transform: uppercase;
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  letter-spacing: 1px;
}

.quick-view:hover {
  background: #fff;
  color: #0a0a0a;
  transform: scale(1.05);
}

.merch-info {
  padding: 1.5rem;
}

.merch-name {
  font-size: 1.2rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
  color: #fff;
}

.merch-category {
  color: #999;
  font-size: 0.9rem;
  margin-bottom: 1rem;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.merch-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 1rem;
  border-top: 1px solid rgba(255, 0, 51, 0.2);
}

.merch-price {
  font-size: 1.5rem;
  font-weight: 900;
  color: #ff0033;
}

.btn-add-cart {
  padding: 0.75rem 1.5rem;
  background: #ff0033;
  border: none;
  color: #fff;
  font-weight: 700;
  font-size: 0.9rem;
  text-transform: uppercase;
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  letter-spacing: 0.5px;
}

.btn-add-cart:hover {
  background: #cc0029;
  transform: translateX(5px);
  box-shadow: 0 5px 20px rgba(255, 0, 51, 0.4);
}

.merch-cta {
  background: rgba(255, 0, 51, 0.1);
  border: 2px solid rgba(255, 0, 51, 0.3);
  padding: 2rem;
  text-align: center;
  border-radius: 10px;
}

.cta-text {
  font-size: 1.5rem;
  font-weight: 700;
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  letter-spacing: 1px;
}

.cta-text i {
  color: #ff0033;
  font-size: 2rem;
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
  
  .merch-grid {
    grid-template-columns: 1fr;
    max-width: 400px;
    margin: 0 auto 4rem;
  }
  
  .cta-text {
    font-size: 1.2rem;
    flex-direction: column;
  }
}
</style>

