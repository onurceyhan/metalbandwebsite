<template>
  <section id="contact" class="contact-section">
    <div class="container">
      <h2 class="section-title glitch" data-text="CONTACT">CONTACT</h2>
      <p class="section-subtitle">Get in touch with us</p>
      
      <div class="contact-content">
        <div class="contact-info">
          <h3 class="info-title">Let's Connect</h3>
          <p class="info-text">
            For booking inquiries, press requests, or general questions, 
            feel free to reach out to us through any of the channels below.
          </p>
          
          <div class="contact-methods">
            <div class="contact-method">
              <div class="method-icon">
                <i class="fas fa-envelope"></i>
              </div>
              <div class="method-details">
                <h4>Email</h4>
                <a href="mailto:booking@steelvengeance.com">booking@steelvengeance.com</a>
              </div>
            </div>
            
            <div class="contact-method">
              <div class="method-icon">
                <i class="fas fa-phone"></i>
              </div>
              <div class="method-details">
                <h4>Phone</h4>
                <a href="tel:+1234567890">+1 (234) 567-890</a>
              </div>
            </div>
            
            <div class="contact-method">
              <div class="method-icon">
                <i class="fas fa-map-marker-alt"></i>
              </div>
              <div class="method-details">
                <h4>Location</h4>
                <p>Los Angeles, CA</p>
              </div>
            </div>
          </div>
          
          <div class="social-links">
            <h4 class="social-title">Follow Us</h4>
            <div class="social-icons">
              <a href="https://facebook.com" target="_blank" class="social-icon">
                <i class="fab fa-facebook"></i>
              </a>
              <a href="https://twitter.com" target="_blank" class="social-icon">
                <i class="fab fa-twitter"></i>
              </a>
              <a href="https://instagram.com" target="_blank" class="social-icon">
                <i class="fab fa-instagram"></i>
              </a>
              <a href="https://youtube.com" target="_blank" class="social-icon">
                <i class="fab fa-youtube"></i>
              </a>
              <a href="https://spotify.com" target="_blank" class="social-icon">
                <i class="fab fa-spotify"></i>
              </a>
            </div>
          </div>
        </div>
        
        <div class="contact-form-wrapper">
          <form @submit.prevent="handleSubmit" class="contact-form">
            <div class="form-group">
              <label for="name">Name</label>
              <input 
                type="text" 
                id="name" 
                v-model="formData.name" 
                required 
                placeholder="Your Name"
              />
            </div>
            
            <div class="form-group">
              <label for="email">Email</label>
              <input 
                type="email" 
                id="email" 
                v-model="formData.email" 
                required 
                placeholder="your@email.com"
              />
            </div>
            
            <div class="form-group">
              <label for="subject">Subject</label>
              <input 
                type="text" 
                id="subject" 
                v-model="formData.subject" 
                required 
                placeholder="What's this about?"
              />
            </div>
            
            <div class="form-group">
              <label for="message">Message</label>
              <textarea 
                id="message" 
                v-model="formData.message" 
                rows="6" 
                required 
                placeholder="Your message..."
              ></textarea>
            </div>
            
            <button type="submit" class="btn-submit" :disabled="isSubmitting">
              <span v-if="!isSubmitting">
                <i class="fas fa-paper-plane"></i>
                Send Message
              </span>
              <span v-else>
                <i class="fas fa-spinner fa-spin"></i>
                Sending...
              </span>
            </button>
            
            <transition name="fade">
              <div v-if="submitMessage" class="submit-message" :class="submitSuccess ? 'success' : 'error'">
                {{ submitMessage }}
              </div>
            </transition>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, reactive } from 'vue'

const formData = reactive({
  name: '',
  email: '',
  subject: '',
  message: ''
})

const isSubmitting = ref(false)
const submitMessage = ref('')
const submitSuccess = ref(false)

const handleSubmit = async () => {
  isSubmitting.value = true
  submitMessage.value = ''
  
  // Simulate form submission
  setTimeout(() => {
    isSubmitting.value = false
    submitSuccess.value = true
    submitMessage.value = 'Thank you! Your message has been sent successfully.'
    
    // Reset form
    formData.name = ''
    formData.email = ''
    formData.subject = ''
    formData.message = ''
    
    // Clear message after 5 seconds
    setTimeout(() => {
      submitMessage.value = ''
    }, 5000)
  }, 2000)
}
</script>

<style scoped>
.contact-section {
  min-height: 100vh;
  padding: 6rem 2rem;
  background: linear-gradient(180deg, #0a0a0a 0%, #0d0d0d 50%, #0a0a0a 100%);
  position: relative;
}

.container {
  max-width: 1200px;
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

.contact-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: start;
}

.contact-info {
  animation: slide-up 0.6s ease-out;
}

.info-title {
  font-size: 2rem;
  font-weight: 700;
  margin-bottom: 1rem;
  color: #ff0033;
  letter-spacing: 2px;
}

.info-text {
  color: #ccc;
  line-height: 1.8;
  margin-bottom: 2rem;
  font-size: 1.05rem;
}

.contact-methods {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  margin-bottom: 3rem;
}

.contact-method {
  display: flex;
  align-items: center;
  gap: 1.5rem;
  padding: 1.5rem;
  background: rgba(26, 26, 26, 0.5);
  border: 1px solid rgba(255, 0, 51, 0.2);
  transition: all 0.3s ease;
}

.contact-method:hover {
  border-color: #ff0033;
  transform: translateX(10px);
  background: rgba(26, 26, 26, 0.8);
}

.method-icon {
  width: 50px;
  height: 50px;
  background: rgba(255, 0, 51, 0.1);
  border: 2px solid #ff0033;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

.method-icon i {
  font-size: 1.5rem;
  color: #ff0033;
}

.method-details h4 {
  font-size: 1.1rem;
  margin-bottom: 0.25rem;
  color: #fff;
}

.method-details a,
.method-details p {
  color: #999;
  text-decoration: none;
  transition: color 0.3s ease;
}

.method-details a:hover {
  color: #ff0033;
}

.social-links {
  padding-top: 2rem;
  border-top: 1px solid rgba(255, 0, 51, 0.2);
}

.social-title {
  font-size: 1.3rem;
  margin-bottom: 1.5rem;
  color: #fff;
  letter-spacing: 1px;
}

.social-icons {
  display: flex;
  gap: 1rem;
}

.social-icon {
  width: 50px;
  height: 50px;
  background: rgba(255, 255, 255, 0.05);
  border: 2px solid rgba(255, 255, 255, 0.2);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #fff;
  font-size: 1.3rem;
  text-decoration: none;
  transition: all 0.3s ease;
}

.social-icon:hover {
  background: #ff0033;
  border-color: #ff0033;
  transform: translateY(-5px);
  box-shadow: 0 5px 20px rgba(255, 0, 51, 0.4);
}

.contact-form-wrapper {
  animation: slide-up 0.6s ease-out 0.2s backwards;
}

.contact-form {
  background: rgba(26, 26, 26, 0.5);
  border: 1px solid rgba(255, 0, 51, 0.2);
  padding: 2.5rem;
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.5rem;
  color: #fff;
  font-weight: 600;
  font-size: 0.95rem;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 1rem;
  background: rgba(0, 0, 0, 0.5);
  border: 1px solid rgba(255, 255, 255, 0.1);
  color: #fff;
  font-size: 1rem;
  font-family: 'Rajdhani', sans-serif;
  transition: all 0.3s ease;
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #ff0033;
  box-shadow: 0 0 20px rgba(255, 0, 51, 0.2);
}

.form-group textarea {
  resize: vertical;
  min-height: 150px;
}

.btn-submit {
  width: 100%;
  padding: 1.25rem;
  background: #ff0033;
  border: none;
  color: #fff;
  font-weight: 700;
  font-size: 1.1rem;
  text-transform: uppercase;
  letter-spacing: 2px;
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.75rem;
}

.btn-submit:hover:not(:disabled) {
  background: #cc0029;
  transform: translateY(-3px);
  box-shadow: 0 5px 30px rgba(255, 0, 51, 0.5);
}

.btn-submit:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}

.submit-message {
  margin-top: 1rem;
  padding: 1rem;
  border-radius: 5px;
  text-align: center;
  font-weight: 600;
}

.submit-message.success {
  background: rgba(0, 255, 0, 0.1);
  border: 1px solid rgba(0, 255, 0, 0.3);
  color: #0f0;
}

.submit-message.error {
  background: rgba(255, 0, 0, 0.1);
  border: 1px solid rgba(255, 0, 0, 0.3);
  color: #f00;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
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
  .contact-content {
    grid-template-columns: 1fr;
    gap: 3rem;
  }
  
  .section-title {
    font-size: 2.5rem;
  }
}
</style>

