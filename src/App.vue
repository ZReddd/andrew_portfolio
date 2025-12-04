<script setup>
import HeroSection from './components/HeroSection.vue'
import ExperienceSection from './components/ExperienceSection.vue'
import PortfolioSection from './components/PortfolioSection.vue'
import AboutSection from './components/AboutSection.vue'
import SkillsSection from './components/SkillsSection.vue'
import FooterSection from './components/FooterSection.vue'
</script>

<template>
  <main class="app">
    <HeroSection />
    <ExperienceSection />
    <PortfolioSection />
    <AboutSection />
    <SkillsSection />
    <FooterSection />
    
    <!-- Floating Totoro -->
    <div class="floating-totoro">
      <img src="/totoro.gif" alt="Totoro" />
    </div>
  </main>
</template>

<style>
.app {
  min-height: 100vh;
  overflow-x: hidden;
}

.floating-totoro {
  position: fixed;
  bottom: 20px;
  right: 20px;
  z-index: 999;
  pointer-events: none;
  opacity: 0.85;
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.floating-totoro:hover {
  opacity: 1;
  transform: scale(1.1);
  pointer-events: auto;
}

.floating-totoro img {
  width: 80px;
  height: auto;
}

@media (max-width: 768px) {
  .floating-totoro img {
    width: 60px;
  }
}
</style>
