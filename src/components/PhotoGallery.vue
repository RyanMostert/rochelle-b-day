<script setup lang="ts">
import { ref, onMounted } from 'vue'

const isVisible = ref(false)

const photos = [
  { id: 1, src: new URL('../assets/Photos/WhatsApp Image 2026-02-27 at 4.31.49 PM.jpeg', import.meta.url).href, alt: 'Herinneringe 1' },
  { id: 2, src: new URL('../assets/Photos/WhatsApp Image 2026-02-27 at 4.31.50 PM (1).jpeg', import.meta.url).href, alt: 'Herinneringe 2' },
  { id: 3, src: new URL('../assets/Photos/WhatsApp Image 2026-02-27 at 4.31.50 PM.jpeg', import.meta.url).href, alt: 'Herinneringe 3' },
  { id: 4, src: new URL('../assets/Photos/WhatsApp Image 2026-02-27 at 4.31.51 PM (1).jpeg', import.meta.url).href, alt: 'Herinneringe 4' },
  { id: 5, src: new URL('../assets/Photos/WhatsApp Image 2026-02-27 at 4.31.51 PM (2).jpeg', import.meta.url).href, alt: 'Herinneringe 5' },
  { id: 6, src: new URL('../assets/Photos/WhatsApp Image 2026-02-27 at 4.31.51 PM.jpeg', import.meta.url).href, alt: 'Herinneringe 6' },
  { id: 7, src: new URL('../assets/Photos/WhatsApp Image 2026-02-27 at 4.31.52 PM (1).jpeg', import.meta.url).href, alt: 'Herinneringe 7' },
  { id: 8, src: new URL('../assets/Photos/WhatsApp Image 2026-02-27 at 4.31.52 PM.jpeg', import.meta.url).href, alt: 'Herinneringe 8' },
]

onMounted(() => {
  setTimeout(() => {
    isVisible.value = true
  }, 300)
})
</script>

<template>
  <section class="gallery-section">
    <h2 class="section-title" :class="{ visible: isVisible }">Herinneringe</h2>
    
    <div class="gallery-wrapper" :class="{ visible: isVisible }">
      <div class="gallery-track">
        <!-- Original set -->
        <div 
          v-for="(photo, index) in photos" 
          :key="`orig-${photo.id}`" 
          class="photo-card"
          :style="{ animationDelay: `${index * 0.1}s` }"
        >
          <div class="photo-frame">
            <img :src="photo.src" :alt="photo.alt" loading="lazy" />
            <div class="photo-overlay">
              <span class="photo-number">{{ index + 1 }}</span>
            </div>
          </div>
          <div class="photo-shine"></div>
        </div>
        <!-- Duplicate set for seamless loop -->
        <div 
          v-for="(photo, index) in photos" 
          :key="`dup-${photo.id}`" 
          class="photo-card"
          aria-hidden="true"
        >
          <div class="photo-frame">
            <img :src="photo.src" :alt="photo.alt" loading="lazy" />
            <div class="photo-overlay">
              <span class="photo-number">{{ index + 1 }}</span>
            </div>
          </div>
          <div class="photo-shine"></div>
        </div>
      </div>
    </div>
    <p class="gallery-hint" :class="{ visible: isVisible }">Kyk hoe pragtig!❤️</p>
  </section>
</template>

<style scoped>
.gallery-section {
  padding: 4rem 0;
  position: relative;
  z-index: 1;
}

.section-title {
  text-align: center;
  font-size: clamp(2rem, 6vw, 3.5rem);
  color: var(--color-secondary);
  margin-bottom: 2rem;
  opacity: 0;
  transform: translateX(-30px);
  transition: all 0.8s ease-out;
}

.section-title.visible {
  opacity: 1;
  transform: translateX(0);
}

.gallery-wrapper {
  overflow-x: hidden;
  overflow-y: hidden;
  padding: 2rem 0;
  margin: 0 -2rem;
  opacity: 0;
  transform: translateX(50px);
  transition: all 0.8s ease-out 0.2s;
}

.gallery-wrapper.visible {
  opacity: 1;
  transform: translateX(0);
}

.gallery-track {
  display: flex;
  gap: 1.5rem;
  padding: 0 2rem;
  width: max-content;
  animation: slideRight 20s linear infinite;
}

.gallery-track:hover {
  animation-play-state: paused;
}

@keyframes slideRight {
  0% { transform: translateX(0); }
  100% { transform: translateX(calc(-50% - 0.75rem)); }
}

.photo-card {
  flex-shrink: 0;
  width: 280px;
  position: relative;
  animation: fadeInUp 0.6s ease-out forwards;
  opacity: 0;
}

.photo-frame {
  position: relative;
  border-radius: var(--radius-lg);
  overflow: hidden;
  box-shadow: var(--shadow-card);
  transition: var(--transition-smooth);
}

.photo-frame::before {
  content: '';
  position: absolute;
  inset: 0;
  border: 3px solid white;
  border-radius: var(--radius-lg);
  z-index: 2;
  pointer-events: none;
}

.photo-card:hover .photo-frame {
  transform: translateY(-10px) rotate(2deg);
  box-shadow: var(--shadow-hover);
}

.photo-frame img {
  width: 100%;
  height: 350px;
  object-fit: cover;
  display: block;
  transition: var(--transition-smooth);
}

.photo-card:hover .photo-frame img {
  transform: scale(1.05);
}

.photo-overlay {
  position: absolute;
  top: 1rem;
  right: 1rem;
  width: 36px;
  height: 36px;
  background: var(--color-primary);
  border-radius: var(--radius-full);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 3;
}

.photo-number {
  color: white;
  font-weight: 600;
  font-size: 0.875rem;
}

.photo-shine {
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    90deg,
    transparent,
    rgba(255, 255, 255, 0.3),
    transparent
  );
  transition: left 0.6s ease;
  pointer-events: none;
  border-radius: var(--radius-lg);
}

.photo-card:hover .photo-shine {
  left: 100%;
}

.gallery-hint {
  text-align: center;
  font-size: 0.875rem;
  color: var(--color-text-light);
  margin-top: 1.5rem;
  opacity: 0;
  transition: opacity 0.5s ease 0.5s;
}

.gallery-hint.visible {
  opacity: 1;
}

@media (max-width: 480px) {
  .gallery-section {
    padding: 2rem 0;
  }
  
  .photo-card {
    width: 220px;
  }
  
  .photo-frame img {
    height: 280px;
  }
}
</style>
