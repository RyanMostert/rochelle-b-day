<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const isVisible = ref(false)
const messageRef = ref<HTMLElement | null>(null)
let observer: IntersectionObserver | null = null

onMounted(() => {
  observer = new IntersectionObserver((entries) => {
    if (entries[0].isIntersecting) {
      isVisible.value = true
      if (messageRef.value && observer) {
        observer.unobserve(messageRef.value)
      }
    }
  }, { threshold: 0.2 })

  if (messageRef.value) {
    observer.observe(messageRef.value)
  }
})

onUnmounted(() => {
  if (observer) {
    observer.disconnect()
  }
})
</script>

<template>
  <section class="message-section" ref="messageRef">
    <div class="message-container">
      <div class="message-content glass" :class="{ visible: isVisible }">
        <div class="decoration-top">
          <span class="heart">💕</span>
        </div>
        
        <h2 class="message-title" :class="{ visible: isVisible }">Gelukkige Verjaarsdag, Rochelle!</h2>
        
        <div class="message-body" :class="{ visible: isVisible }">
          <p class="message-paragraph">
            Vandag gaan alles oor jou — 'n waarlik wonderlike mens wat soveel lig en vreugde bring vir almal om jou. 
            Jou vriendelikheid, jou glimlag en jou ongelooflike gees maak die wêreld 'n beter plek.
          </p>
          
          <p class="message-paragraph">
            Mag hierdie nuwe jaar van jou lewe gevul wees met eindelose laggies, avonture en al die geluk wat jy verdien. 
            Mag jou drome vlerke kry en jou hart gevul wees met verwondering.
          </p>
          
          <p class="message-paragraph">
            Hier is vir nog 'n jaar van herinneringe maak, vreugde versprei en om die wonderlike siel te wees wat jy is. 
            Jy is geliefd, jy word waardeer, en jy is absoluut amazing!
          </p>
        </div>
        
        <div class="signature" :class="{ visible: isVisible }">
          <p>Met al my liefde,</p>
          <span class="signature-name">Jou Spesiale Iemand</span>
        </div>
        
        <div class="decoration-bottom">
          <span class="sparkle">✨</span>
          <span class="sparkle">💖</span>
          <span class="sparkle">✨</span>
        </div>
      </div>
      
      <div class="floating-elements">
        <span class="float-element element-1">🎁</span>
        <span class="float-element element-2">🎂</span>
        <span class="float-element element-3">🥂</span>
        <span class="float-element element-4">🌟</span>
      </div>
    </div>
  </section>
</template>

<style scoped>
.message-section {
  padding: 4rem 1.5rem 6rem;
  position: relative;
  z-index: 1;
}

.message-container {
  max-width: 700px;
  margin: 0 auto;
  position: relative;
}

.message-content {
  border-radius: var(--radius-lg);
  padding: 3rem;
  text-align: center;
  opacity: 0;
  transform: translateY(50px);
  transition: all 0.8s ease-out;
}

.message-content.visible {
  opacity: 1;
  transform: translateY(0);
}

.decoration-top,
.decoration-bottom {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 1.5rem;
}

.heart {
  font-size: 2rem;
  animation: pulse 1.5s ease-in-out infinite;
}

.sparkle {
  font-size: 1.5rem;
}

.message-title {
  font-size: clamp(2rem, 5vw, 3rem);
  color: var(--color-primary);
  margin-bottom: 2rem;
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.6s ease-out 0.2s;
}

.message-title.visible {
  opacity: 1;
  transform: translateY(0);
}

.message-body {
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.6s ease-out 0.4s;
}

.message-body.visible {
  opacity: 1;
  transform: translateY(0);
}

.message-paragraph {
  font-size: clamp(1rem, 2.5vw, 1.125rem);
  color: var(--color-text);
  line-height: 1.8;
  margin-bottom: 1.5rem;
}

.message-paragraph:last-child {
  margin-bottom: 0;
}

.signature {
  margin-top: 2.5rem;
  padding-top: 2rem;
  border-top: 2px dashed var(--color-pink-soft);
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.6s ease-out 0.6s;
}

.signature.visible {
  opacity: 1;
  transform: translateY(0);
}

.signature p {
  font-style: italic;
  color: var(--color-text-light);
  margin-bottom: 0.5rem;
}

.signature-name {
  font-family: var(--font-display);
  font-size: 1.75rem;
  color: var(--color-secondary);
}

.floating-elements {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  pointer-events: none;
}

.float-element {
  position: absolute;
  font-size: 2.5rem;
  animation: float 4s ease-in-out infinite;
}

.element-1 { top: 10%; left: -20px; animation-delay: 0s; }
.element-2 { top: 30%; right: -20px; animation-delay: 1s; }
.element-3 { bottom: 20%; left: -10px; animation-delay: 2s; }
.element-4 { bottom: 10%; right: -15px; animation-delay: 1.5s; }

@media (max-width: 480px) {
  .message-section {
    padding: 2rem 1rem 4rem;
  }
  
  .message-content {
    padding: 2rem 1.5rem;
  }
  
  .float-element {
    font-size: 1.75rem;
  }
}
</style>
