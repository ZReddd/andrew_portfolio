<script setup>
import { ref, onMounted } from 'vue'

const base = import.meta.env.BASE_URL
const profileImage = `${base}profile.jpg`

const isVisible = ref(false)
const sectionRef = ref(null)

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          isVisible.value = true
        }
      })
    },
    { threshold: 0.2 }
  )

  if (sectionRef.value) {
    observer.observe(sectionRef.value)
  }
})
</script>

<template>
  <section id="about" class="about" ref="sectionRef">
    <div class="about-container">
      <div class="section-header" :class="{ 'is-visible': isVisible }">
        <span class="section-number">03</span>
        <div class="section-title-wrapper">
          <h2 class="section-title">About Me</h2>
          <span class="section-subtitle">The person behind the code</span>
        </div>
        <div class="section-line"></div>
      </div>

      <div class="about-content">
        <div class="about-image-wrapper" :class="{ 'is-visible': isVisible }">
          <div class="about-image">
            <img :src="profileImage" alt="Andrew Cheng" />
          </div>
          <div class="image-decoration"></div>
        </div>

        <div class="about-text" :class="{ 'is-visible': isVisible }">
          <p class="about-intro">
            Thanks for scrolling this far! 🎉 You actually looked at my work — that means a lot.
          </p>
          
          <p class="about-description">
            I genuinely love building products, especially on the backend. There's something 
            satisfying about crafting business logic that actually solves real problems. 
            I enjoy the challenge of turning complex requirements into clean, working systems.
          </p>

          <p class="about-description">
            Outside of coding, you'll find me at the gym 🏋️, on the basketball court 🏀, 
            or deep in crypto research 📈. But honestly? My true passion is FOOD. 
            I'm always hunting for the next great meal.
          </p>

          <p class="about-description about-cta">
            Got a restaurant recommendation? A startup idea? Or just want to chat? 
            <strong>Please reach out!</strong> I'd love to grab coffee and hear what you're working on.
          </p>

          <div class="about-details">
            <div class="detail-item">
              <span class="detail-label">Location</span>
              <span class="detail-value">Adelaide, Australia</span>
            </div>
            <div class="detail-item">
              <span class="detail-label">Email</span>
              <span class="detail-value">a88615123@gmail.com</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.about {
  padding: 8rem 4rem;
  background: var(--color-bg);
  position: relative;
}

.about::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 1px;
  background: var(--color-border);
}

.about-container {
  max-width: 1100px;
  margin: 0 auto;
}

/* Section Header */
.section-header {
  display: flex;
  align-items: center;
  gap: 1.5rem;
  margin-bottom: 4rem;
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s var(--ease-out-expo);
}

.section-header.is-visible {
  opacity: 1;
  transform: translateY(0);
}

.section-number {
  font-family: var(--font-display);
  font-size: 0.9rem;
  color: var(--color-accent);
  font-style: italic;
}

.section-title-wrapper {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
}

.section-title {
  font-family: var(--font-display);
  font-size: 2rem;
  font-weight: 400;
  letter-spacing: 0.02em;
  color: var(--color-text);
}

.section-subtitle {
  font-size: 0.8rem;
  font-weight: 300;
  color: var(--color-text-muted);
  letter-spacing: 0.05em;
}

.section-line {
  flex: 1;
  height: 1px;
  background: var(--color-border);
}

/* About Content */
.about-content {
  display: grid;
  grid-template-columns: 300px 1fr;
  gap: 5rem;
  align-items: start;
}

/* Image */
.about-image-wrapper {
  position: relative;
  opacity: 0;
  transform: translateY(40px);
  transition: all 0.8s var(--ease-out-expo);
  transition-delay: 0.2s;
}

.about-image-wrapper.is-visible {
  opacity: 1;
  transform: translateY(0);
}

.about-image {
  position: relative;
  z-index: 2;
  border-radius: 4px;
  overflow: hidden;
  aspect-ratio: 3 / 4;
}

.about-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: grayscale(20%);
  transition: filter 0.5s ease;
}

.about-image:hover img {
  filter: grayscale(0%);
}

.image-decoration {
  position: absolute;
  top: 20px;
  left: 20px;
  right: -20px;
  bottom: -20px;
  border: 1px solid var(--color-accent);
  border-radius: 4px;
  z-index: 1;
  opacity: 0.5;
}

/* Text */
.about-text {
  opacity: 0;
  transform: translateY(40px);
  transition: all 0.8s var(--ease-out-expo);
  transition-delay: 0.3s;
}

.about-text.is-visible {
  opacity: 1;
  transform: translateY(0);
}

.about-intro {
  font-family: var(--font-display);
  font-size: 1.5rem;
  font-weight: 400;
  line-height: 1.6;
  color: var(--color-text);
  margin-bottom: 1.5rem;
}

.about-description {
  font-size: 1rem;
  font-weight: 300;
  line-height: 1.8;
  color: var(--color-text-secondary);
  margin-bottom: 1.25rem;
}

.about-cta {
  color: var(--color-text);
  background: var(--color-bg-secondary);
  padding: 1rem 1.25rem;
  border-radius: 4px;
  border-left: 3px solid var(--color-accent);
}

.about-cta strong {
  color: var(--color-accent);
}

.about-details {
  display: flex;
  gap: 3rem;
  margin-top: 2.5rem;
  padding-top: 2rem;
  border-top: 1px solid var(--color-border);
}

.detail-item {
  display: flex;
  flex-direction: column;
  gap: 0.35rem;
}

.detail-label {
  font-size: 0.75rem;
  font-weight: 400;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--color-text-muted);
}

.detail-value {
  font-size: 0.95rem;
  color: var(--color-text);
}

/* Responsive */
@media (max-width: 900px) {
  .about {
    padding: 6rem 2rem;
  }

  .about-content {
    grid-template-columns: 1fr;
    gap: 3rem;
  }

  .about-image-wrapper {
    max-width: 280px;
    margin: 0 auto;
  }

  .about-details {
    flex-direction: column;
    gap: 1.5rem;
  }
}
</style>

