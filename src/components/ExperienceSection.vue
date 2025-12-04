<script setup>
import { ref, onMounted } from 'vue'

const base = import.meta.env.BASE_URL

const isVisible = ref(false)
const sectionRef = ref(null)

const experiences = [
  {
    period: '2025 — Present',
    title: 'Junior Software Developer',
    company: 'Redshift Creative',
    location: 'Adelaide, Australia',
    highlights: [
      'Built a full-stack salary packaging CRM system using Laravel, Vue.js, and Vuetify — handling end-to-end workflows from data entry to approval, plus a tax calculation engine that automated complex computations.',
      'Developed RESTful APIs for a referral partner portal, enabling vehicle dealers and external partners to submit leads and track application statuses in real-time.',
      'Collaborated directly with clients and senior engineers to gather requirements, propose solutions, and deliver features — including full-stack development, testing, and WordPress customisations.'
    ]
  },
  {
    period: '2024 — Present',
    title: 'Software Engineer',
    company: 'The University of Queensland',
    location: 'Brisbane, Australia',
    highlights: [
      'Designed and developed a hospital CRM system for the Movement Behaviour Questionnaire (MBQ), enabling healthcare professionals to record and track children\'s behavioural and health histories.',
      'Built the full stack with React.js frontend and Node.js/Express backend, integrated with MongoDB for scalable and secure data management.',
      'Delivered web-based questionnaire and data visualisation tools, collaborating with researchers, clinicians, and engineers to improve accessibility and system performance.'
    ]
  }
]

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
  <section id="experience" class="experience" ref="sectionRef">
    <div class="experience-container">
      <div class="section-header" :class="{ 'is-visible': isVisible }">
        <span class="section-number">01</span>
        <div class="section-title-wrapper">
          <h2 class="section-title">Experience</h2>
          <span class="section-subtitle">Where I've worked</span>
        </div>
        <div class="section-line"></div>
      </div>

      <div class="experience-grid">
        <div 
          v-for="(exp, index) in experiences" 
          :key="index"
          class="experience-item"
          :class="{ 'is-visible': isVisible }"
          :style="{ transitionDelay: `${0.2 + index * 0.15}s` }"
        >
          <span class="exp-period">{{ exp.period }}</span>
          <div class="exp-content">
            <h3 class="exp-title">{{ exp.title }}</h3>
            <div class="exp-company">
              <span>{{ exp.company }}</span>
              <span class="exp-divider">·</span>
              <span class="exp-location">{{ exp.location }}</span>
            </div>
            <ul class="exp-highlights">
              <li v-for="(highlight, hIndex) in exp.highlights" :key="hIndex">
                {{ highlight }}
              </li>
            </ul>
          </div>
        </div>
      </div>

      <div class="education" :class="{ 'is-visible': isVisible }">
        <div class="edu-label">Education</div>
        <div class="edu-content">
          <div class="edu-header">
            <img :src="`${base}uq-logo.png`" alt="UQ" class="edu-logo" />
            <div class="edu-info">
              <span class="edu-degree">Master of Computer Science</span>
              <span class="edu-school">The University of Queensland, 2022 — 2024</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.experience {
  padding: 8rem 4rem;
  background: var(--color-bg);
  position: relative;
}

.experience::before {
  content: '';
  position: absolute;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 1px;
  height: 80px;
  background: linear-gradient(to bottom, transparent, var(--color-border));
}

.experience-container {
  max-width: 1000px;
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

/* Experience Grid */
.experience-grid {
  display: flex;
  flex-direction: column;
  gap: 3rem;
  margin-bottom: 4rem;
}

.experience-item {
  display: grid;
  grid-template-columns: 180px 1fr;
  gap: 3rem;
  padding-bottom: 3rem;
  border-bottom: 1px solid var(--color-border);
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s var(--ease-out-expo);
}

.experience-item.is-visible {
  opacity: 1;
  transform: translateY(0);
}

.exp-period {
  font-size: 0.85rem;
  font-weight: 400;
  color: var(--color-text-secondary);
  letter-spacing: 0.05em;
}

.exp-title {
  font-family: var(--font-display);
  font-size: 1.4rem;
  font-weight: 400;
  color: var(--color-text);
  margin-bottom: 0.5rem;
}

.exp-company {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  margin-bottom: 1rem;
  font-size: 0.9rem;
  color: var(--color-accent-dim);
}

.exp-divider {
  color: var(--color-text-muted);
}

.exp-location {
  color: var(--color-text-muted);
}

.exp-highlights {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.exp-highlights li {
  font-size: 0.95rem;
  font-weight: 300;
  line-height: 1.7;
  color: var(--color-text-secondary);
  padding-left: 1.25rem;
  position: relative;
}

.exp-highlights li::before {
  content: '';
  position: absolute;
  left: 0;
  top: 0.6rem;
  width: 4px;
  height: 4px;
  background: var(--color-accent);
  border-radius: 50%;
}

/* Education */
.education {
  display: flex;
  align-items: flex-start;
  gap: 3rem;
  margin-top: 3rem;
  padding-top: 3rem;
  border-top: 1px solid var(--color-border);
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.8s var(--ease-out-expo);
  transition-delay: 0.5s;
}

.education.is-visible {
  opacity: 1;
  transform: translateY(0);
}

.edu-label {
  font-size: 0.75rem;
  font-weight: 400;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--color-text-muted);
  min-width: 180px;
}

.edu-content {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
}

.edu-header {
  display: flex;
  align-items: center;
  gap: 1.25rem;
}

.edu-logo {
  width: 50px;
  height: 50px;
  object-fit: contain;
  border-radius: 4px;
}

.edu-info {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
}

.edu-degree {
  font-family: var(--font-display);
  font-size: 1.1rem;
  color: var(--color-text);
}

.edu-school {
  font-size: 0.85rem;
  color: var(--color-text-secondary);
}

/* Responsive */
@media (max-width: 768px) {
  .experience {
    padding: 6rem 2rem;
  }

  .experience-item {
    grid-template-columns: 1fr;
    gap: 0.75rem;
  }

  .education {
    flex-direction: column;
    gap: 0.75rem;
  }

  .edu-label {
    min-width: auto;
  }
}
</style>

