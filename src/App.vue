<script setup lang="ts">
import HeroSection from './components/HeroSection.vue'
import PhotoGallery from './components/PhotoGallery.vue'
import BirthdayMessage from './components/BirthdayMessage.vue'
</script>

<template>
  <main class="birthday-site">
    <HeroSection />
    <PhotoGallery />
    <BirthdayMessage />
  </main>
</template>

<style scoped>
.birthday-site {
  min-height: 100vh;
  position: relative;
  overflow-x: hidden;
}

.birthday-site::before {
  content: '';
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: 
    radial-gradient(circle at 20% 20%, rgba(255, 107, 157, 0.1) 0%, transparent 50%),
    radial-gradient(circle at 80% 80%, rgba(212, 165, 255, 0.1) 0%, transparent 50%),
    radial-gradient(circle at 50% 50%, rgba(255, 234, 167, 0.05) 0%, transparent 70%);
  pointer-events: none;
  z-index: 0;
}
</style>
