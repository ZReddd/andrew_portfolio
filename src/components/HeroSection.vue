<script setup>
import { ref, onMounted } from 'vue'

const isLoaded = ref(false)
const imageLoaded = ref(false)

// Background image path - place your image at public/background.jpg
const backgroundImage = '/background.jpg'

onMounted(() => {
  // Check if image exists
  const img = new Image()
  img.onload = () => {
    imageLoaded.value = true
  }
  img.src = backgroundImage
  
  setTimeout(() => {
    isLoaded.value = true
  }, 100)
})
</script>

<template>
  <section class="hero">
    <div class="hero-background">
      <img 
        v-show="imageLoaded" 
        :src="backgroundImage" 
        alt="" 
        class="hero-bg-image" 
      />
      <div class="hero-overlay"></div>
    </div>
    
    <nav class="nav" :class="{ 'is-visible': isLoaded }">
      <div class="nav-content">
        <a href="#" class="nav-logo">
          <img src="/logo.gif" alt="Logo" class="nav-logo-img" />
        </a>
        <div class="nav-links">
          <a href="#experience">Experience</a>
          <a href="#portfolio">Portfolio</a>
          <a href="#about">About</a>
          <a href="#skills">Skills</a>
        </div>
      </div>
    </nav>

    <div class="hero-content">
      <div class="hero-intro" :class="{ 'is-visible': isLoaded }">
        <span class="hero-greeting">Hello, I'm</span>
      </div>
      
      <h1 class="hero-name" :class="{ 'is-visible': isLoaded }">
        Andrew Cheng
      </h1>
      
      <div class="hero-title" :class="{ 'is-visible': isLoaded }">
        <span class="hero-line"></span>
        <span class="hero-role">Software Engineer</span>
      </div>
      
      <p class="hero-description" :class="{ 'is-visible': isLoaded }">
        Full-stack Software Engineer based in Adelaide, specialising in 
        SaaS and B2B platforms. Currently building CRM systems and web 
        applications at Redshift Creative, while supporting research 
        platforms at The University of Queensland.
      </p>

      <div class="hero-scroll" :class="{ 'is-visible': isLoaded }">
        <div class="scroll-line"></div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.hero {
  position: relative;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

.hero-background {
  position: absolute;
  inset: 0;
  z-index: 0;
}

.hero-bg-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
  opacity: 0.65;
  filter: saturate(0.9) brightness(1.1);
}

.hero-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(
    to bottom,
    rgba(12, 11, 10, 0.3) 0%,
    rgba(12, 11, 10, 0.6) 50%,
    rgba(12, 11, 10, 0.95) 100%
  );
}

/* Navigation */
.nav {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
  padding: 2rem 4rem;
  opacity: 0;
  transform: translateY(-20px);
  transition: all 0.8s var(--ease-out-expo);
  transition-delay: 0.8s;
}

.nav.is-visible {
  opacity: 1;
  transform: translateY(0);
}

.nav-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1400px;
  margin: 0 auto;
}

.nav-logo {
  display: flex;
  align-items: center;
  transition: transform 0.3s ease, opacity 0.3s ease;
}

.nav-logo:hover {
  transform: scale(1.1);
  opacity: 1;
}

.nav-logo-img {
  height: 40px;
  width: auto;
  object-fit: contain;
}

.nav-links {
  display: flex;
  gap: 3rem;
}

.nav-links a {
  font-size: 0.85rem;
  font-weight: 300;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--color-text-secondary);
  transition: color 0.3s ease;
}

.nav-links a:hover {
  color: var(--color-text);
  opacity: 1;
}

/* Hero Content */
.hero-content {
  position: relative;
  z-index: 1;
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 8rem 4rem 4rem;
  max-width: 900px;
}

.hero-intro {
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s var(--ease-out-expo);
  transition-delay: 0.2s;
}

.hero-intro.is-visible {
  opacity: 1;
  transform: translateY(0);
}

.hero-greeting {
  font-size: 0.9rem;
  font-weight: 300;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--color-text-secondary);
}

.hero-name {
  font-family: var(--font-display);
  font-size: clamp(3rem, 10vw, 6rem);
  font-weight: 300;
  letter-spacing: -0.02em;
  line-height: 1.1;
  margin: 0.5rem 0 1.5rem;
  color: var(--color-text);
  text-shadow: 0 2px 20px rgba(0, 0, 0, 0.5);
  opacity: 0;
  transform: translateY(40px);
  transition: all 1s var(--ease-out-expo);
  transition-delay: 0.3s;
}

.hero-name.is-visible {
  opacity: 1;
  transform: translateY(0);
}

.hero-title {
  display: flex;
  align-items: center;
  gap: 1.5rem;
  margin-bottom: 2rem;
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s var(--ease-out-expo);
  transition-delay: 0.5s;
}

.hero-title.is-visible {
  opacity: 1;
  transform: translateY(0);
}

.hero-line {
  width: 60px;
  height: 1px;
  background: var(--color-accent);
}

.hero-role {
  font-size: 1.1rem;
  font-weight: 300;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--color-accent);
}

.hero-description {
  font-size: 1.05rem;
  font-weight: 300;
  line-height: 1.8;
  color: var(--color-text-secondary);
  max-width: 580px;
  text-shadow: 0 1px 10px rgba(0, 0, 0, 0.4);
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s var(--ease-out-expo);
  transition-delay: 0.6s;
}

.hero-description.is-visible {
  opacity: 1;
  transform: translateY(0);
}

/* Scroll Indicator */
.hero-scroll {
  position: absolute;
  bottom: 3rem;
  left: 4rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.8s var(--ease-out-expo);
  transition-delay: 1s;
}

.hero-scroll.is-visible {
  opacity: 1;
  transform: translateY(0);
}

.scroll-line {
  width: 1px;
  height: 50px;
  background: linear-gradient(to bottom, var(--color-accent), transparent);
  position: relative;
}

.scroll-line::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 20px;
  background: var(--color-accent);
  animation: scrollDown 1.8s ease-in-out infinite;
}

@keyframes scrollDown {
  0% {
    opacity: 0;
    transform: translateY(-10px);
  }
  30% {
    opacity: 1;
  }
  100% {
    opacity: 0;
    transform: translateY(50px);
  }
}

/* Responsive */
@media (max-width: 768px) {
  .nav {
    padding: 1.5rem 2rem;
  }
  
  .nav-links {
    gap: 1.5rem;
  }
  
  .hero-content {
    padding: 6rem 2rem 3rem;
  }
  
  .hero-scroll {
    left: 2rem;
    bottom: 2rem;
  }
}
</style>

