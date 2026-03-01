<template>
  <section class="hero">
    <div class="hero-content" :class="{ visible: isVisible }">
      <div class="cake-container">
        <div class="cake">
          <div class="candle">
            <div class="flame"></div>
          </div>
          <div class="cake-body">
            <div class="cake-layer layer-1"></div>
            <div class="cake-layer layer-2"></div>
            <div class="cake-layer layer-3"></div>
          </div>
          <div class="plate"></div>
        </div>
      </div>
      
      <h1 class="title">
        <span class="happy">Gelukkige</span>
        <span class="birthday">Verjaarsdag</span>
      </h1>
      
      <h2 class="name">Rochelle!</h2>
      <h2 class="age">
        <span class="old-age" :class="{ struck }">22</span>
        <span class="new-age" :class="{ visible: showNew }">21</span>
      </h2>
      
      <p class="subtitle">Vier jou spesiale dag</p>
      
      <div class="decorations">
        <span class="confetti confetti-1" style="--d: 0s; --x: 10%; --y: 10%;" aria-hidden="true">🎉</span>
        <span class="confetti confetti-2" style="--d: 0.5s; --x: 85%; --y: 15%;" aria-hidden="true">🎊</span>
        <span class="confetti confetti-3" style="--d: 1.2s; --x: 5%; --y: 25%;" aria-hidden="true">✨</span>
        <span class="confetti confetti-4" style="--d: 1.8s; --x: 90%; --y: 20%;" aria-hidden="true">💖</span>
        <span class="confetti confetti-5" style="--d: 2.5s; --x: 75%; --y: 8%;" aria-hidden="true">🎈</span>
        <span class="confetti confetti-6" style="--d: 3s; --x: 15%; --y: 35%;" aria-hidden="true">🌸</span>
      </div>
    </div>
    
    <button class="scroll-indicator" :class="{ visible: isVisible }" @click="scrollToGallery">
      <span>Rol af om te vier</span>
      <div class="arrow">↓</div>
    </button>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const isVisible = ref(false)
const struck = ref(false)
const showNew = ref(false)

let timer: ReturnType<typeof setTimeout>

function runLoop() {
  struck.value = false
  showNew.value = false

  timer = setTimeout(() => {
    struck.value = true

    timer = setTimeout(() => {
      showNew.value = true

      timer = setTimeout(() => {
        struck.value = false
        showNew.value = false

        timer = setTimeout(runLoop, 600)
      }, 1800)
    }, 700)
  }, 1000)
}

const scrollToGallery = () => {
  const gallery = document.querySelector('.gallery-section')
  gallery?.scrollIntoView({ behavior: 'smooth' })
}

onMounted(() => {
  setTimeout(() => {
    isVisible.value = true
  }, 100)
  runLoop()
})

onUnmounted(() => clearTimeout(timer))
</script>

<style scoped>
.hero {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  position: relative;
  padding: 2rem;
}

.hero-content {
  text-align: center;
  opacity: 0;
  transform: translateY(30px);
  transition: all 1s ease-out;
}

.hero-content.visible {
  opacity: 1;
  transform: translateY(0);
}

.cake-container {
  margin-bottom: 2rem;
}

.cake {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  animation: float 3s ease-in-out infinite;
}

.candle {
  width: 8px;
  height: 40px;
  background: linear-gradient(to right, #ff6b9d, #c44569);
  border-radius: 4px;
  position: relative;
  margin-bottom: -5px;
  z-index: 2;
}

.flame {
  position: absolute;
  top: -20px;
  left: 50%;
  transform: translateX(-50%);
  width: 16px;
  height: 24px;
  background: radial-gradient(ellipse at bottom, #ffd93d, #ff6b9d);
  border-radius: 50% 50% 50% 50% / 60% 60% 40% 40%;
  animation: flicker 0.5s ease-in-out infinite alternate;
}

@keyframes flicker {
  0% { transform: translateX(-50%) scale(1); opacity: 1; }
  100% { transform: translateX(-50%) scale(1.1); opacity: 0.8; }
}

.cake-body {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.cake-layer {
  border-radius: 8px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
}

.layer-1 {
  width: 140px;
  height: 35px;
  background: linear-gradient(135deg, #ff6b9d, #c44569);
  margin-bottom: -8px;
}

.layer-2 {
  width: 110px;
  height: 30px;
  background: linear-gradient(135deg, #f8c8dc, #ff6b9d);
  margin-bottom: -8px;
}

.layer-3 {
  width: 80px;
  height: 25px;
  background: linear-gradient(135deg, #ffd93d, #ff6b9d);
}

.plate {
  width: 160px;
  height: 12px;
  background: rgba(255, 255, 255, 0.6);
  border-radius: 50%;
  margin-top: -2px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
}

.title {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
  margin-bottom: 0.5rem;
}

.happy {
  font-size: clamp(2.5rem, 8vw, 5rem);
  color: var(--color-primary);
  text-shadow: 2px 2px 0 var(--color-pink-soft);
}

.birthday {
  font-size: clamp(2rem, 6vw, 4rem);
  color: var(--color-secondary);
}

.name {
  font-size: clamp(3rem, 12vw, 7rem);
  background: linear-gradient(135deg, var(--color-primary), var(--color-purple-soft), var(--color-accent));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  margin: 0.25rem 0;
  animation: pulse 2s ease-in-out infinite;
}

.age {
  font-size: clamp(2rem, 8vw, 5rem);
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0;
  margin: 0.25rem 0;
}

.old-age {
  color: var(--color-text-light);
  position: relative;
}

.old-age::after {
  content: '';
  position: absolute;
  left: -4px;
  right: -4px;
  top: 50%;
  height: 3px;
  border-radius: 2px;
  background: var(--color-primary);
  transform: translateY(-50%) rotate(-1.5deg);
  clip-path: inset(0 100% 0 0);
  transition: clip-path 0.65s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.old-age.struck::after {
  clip-path: inset(0 0% 0 0);
}

.new-age {
  color: var(--color-primary);
  display: inline-block;
  overflow: hidden;
  max-width: 0;
  opacity: 0;
  margin-left: 0;
  transform: translateX(-6px);
  transition:
    max-width 0.55s cubic-bezier(0.34, 1.4, 0.64, 1),
    margin-left 0.55s cubic-bezier(0.34, 1.4, 0.64, 1),
    opacity 0.35s ease,
    transform 0.55s cubic-bezier(0.34, 1.4, 0.64, 1);
}

.new-age.visible {
  max-width: 3ch;
  opacity: 1;
  margin-left: 0.75rem;
  transform: translateX(0);
}

.subtitle {
  font-size: clamp(1rem, 3vw, 1.5rem);
  color: var(--color-text-light);
  font-weight: 300;
}

.decorations {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  pointer-events: none;
  overflow: hidden;
}

.confetti {
  position: absolute;
  top: var(--y);
  left: var(--x);
  font-size: 2rem;
  animation: float 4s ease-in-out infinite;
  animation-delay: var(--d);
}

.scroll-indicator {
  position: absolute;
  bottom: 2rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  opacity: 0;
  transition: opacity 0.5s ease 1.5s;
  background: none;
  border: none;
  cursor: pointer;
}

.scroll-indicator:focus-visible {
  outline: 2px solid var(--color-primary);
  outline-offset: 4px;
  border-radius: var(--radius-sm);
}

.scroll-indicator.visible {
  opacity: 1;
}

.scroll-indicator span {
  font-size: 0.875rem;
  color: var(--color-text-light);
}

.arrow {
  font-size: 1.5rem;
  color: var(--color-primary);
  animation: bounce 2s ease-in-out infinite;
}

@keyframes bounce {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(8px); }
}

@media (max-width: 480px) {
  .hero {
    padding: 1rem;
  }
  
  .confetti {
    font-size: 1.5rem;
  }
}
</style>
