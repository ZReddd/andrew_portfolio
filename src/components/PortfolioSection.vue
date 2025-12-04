<script setup>
import { ref, onMounted } from 'vue'

const base = import.meta.env.BASE_URL

const isVisible = ref(false)
const sectionRef = ref(null)

const projects = [
  {
    id: 1,
    title: 'MBQ Project',
    category: 'Healthcare Platform',
    description: 'A hospital CRM system developed for The University of Queensland and Queensland Children\'s Hospital. I designed and built a comprehensive platform that enables healthcare professionals and researchers to record, track, and analyse children\'s movement behaviour and health histories through the Movement Behaviour Questionnaire.',
    highlights: [
      'Built an intuitive questionnaire interface for parents and clinicians to input behavioural data',
      'Developed data visualisation dashboards providing actionable insights for researchers',
      'Ensured secure, scalable data management compliant with healthcare standards'
    ],
    tags: ['React.js', 'Node.js', 'Express', 'MongoDB'],
    image: `${base}mbq.JPG`,
    link: 'https://www.mbqproject.com/',
    hasLink: true,
    note: 'To explore the full CRM system, you\'ll need to join the MBQ Project. But feel free to check it out and see how we\'re helping track and improve children\'s movement behaviour!'
  },
  {
    id: 2,
    title: 'Vehicle Solutions CRM',
    category: 'Enterprise System',
    description: 'A full-stack CRM system built for Vehicle Solutions at Redshift Creative. This internal platform streamlines the entire salary packaging workflow — from BDM application submissions to financial approvals. The system handles complex tax calculations for Novated Leasing and Chattel Mortgage, generates professional invoices, and manages the complete application lifecycle.',
    highlights: [
      'Automated tax saving calculations and salary packaging computations',
      'Built Blade-templated invoice generation with PDF export',
      'Designed intuitive forms for BDMs to rapidly submit and track applications'
    ],
    tags: ['Laravel', 'Vue.js', 'Vuetify', 'MySQL', 'Blade'],
    image: `${base}crm.jpg`,
    link: 'https://vehiclesolutions.com.au/',
    hasLink: true,
    linkText: 'Visit Calculator',
    note: 'The CRM is internal, but I built the public Calculator API — now used by multiple car dealerships. This system also supports SA Government employees to get Novated Leases & Chattel Mortgages through VSA partnership.'
  },
  {
    id: 3,
    title: 'Aussie Grocery Compare',
    category: 'Side Project',
    description: 'A real-time price comparison tool for Australian supermarkets. This ongoing personal project fetches live product data from Coles, Aldi, and Woolworths APIs, allowing users to compare prices instantly and find the best deals across major retailers.',
    highlights: [
      'Real-time API integration with Coles, Aldi, and Woolworths',
      'Built with Vue.js frontend and .NET backend',
      'Live price tracking and comparison across multiple retailers'
    ],
    tags: ['Vue.js', '.NET', 'REST APIs', 'Web Scraping'],
    image: `${base}grocery.jpg`,
    link: null,
    hasLink: false,
    note: 'Ongoing side project — actively in development.'
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
    { threshold: 0.1 }
  )

  if (sectionRef.value) {
    observer.observe(sectionRef.value)
  }
})
</script>

<template>
  <section id="portfolio" class="portfolio" ref="sectionRef">
    <div class="portfolio-container">
      <div class="section-header" :class="{ 'is-visible': isVisible }">
        <span class="section-number">02</span>
        <div class="section-title-wrapper">
          <h2 class="section-title">Projects</h2>
          <span class="section-subtitle">What I've built</span>
        </div>
        <div class="section-line"></div>
      </div>

      <div class="projects-grid">
        <article 
          v-for="(project, index) in projects" 
          :key="project.id"
          class="project-card"
          :class="{ 'is-visible': isVisible }"
          :style="{ transitionDelay: `${0.2 + index * 0.15}s` }"
        >
          <div class="project-image">
            <img 
              v-if="project.image" 
              :src="project.image" 
              :alt="project.title"
              class="project-img"
            />
            <div v-else class="project-placeholder">
              <span class="placeholder-number">0{{ project.id }}</span>
            </div>
          </div>
          
          <div class="project-content">
            <span class="project-category">{{ project.category }}</span>
            <h3 class="project-title">{{ project.title }}</h3>
            <p class="project-description">{{ project.description }}</p>
            
            <ul v-if="project.highlights && project.highlights.length" class="project-highlights">
              <li v-for="(highlight, hIndex) in project.highlights" :key="hIndex">
                {{ highlight }}
              </li>
            </ul>
            
            <div class="project-tags">
              <span v-for="tag in project.tags" :key="tag" class="tag">
                {{ tag }}
              </span>
            </div>

            <div class="project-footer">
              <a 
                v-if="project.hasLink" 
                :href="project.link" 
                target="_blank"
                class="project-link"
              >
                <span>{{ project.linkText || 'View Live Site' }}</span>
                <svg width="16" height="16" viewBox="0 0 16 16" fill="none">
                  <path d="M4 12L12 4M12 4H6M12 4V10" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
                </svg>
              </a>
              <span v-else class="project-private">
                <svg width="14" height="14" viewBox="0 0 24 24" fill="none">
                  <rect x="3" y="11" width="18" height="11" rx="2" stroke="currentColor" stroke-width="1.5"/>
                  <path d="M7 11V7a5 5 0 0110 0v4" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
                </svg>
                <span>Internal System</span>
              </span>
              <p v-if="project.note" class="project-note">{{ project.note }}</p>
            </div>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<style scoped>
.portfolio {
  padding: 8rem 4rem;
  background: var(--color-bg-secondary);
  position: relative;
}

.portfolio::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 1px;
  background: var(--color-border);
}

.portfolio-container {
  max-width: 1200px;
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

/* Projects Grid */
.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(340px, 1fr));
  gap: 2rem;
}

.project-card {
  background: var(--color-bg-card);
  border: 1px solid var(--color-border);
  border-radius: 4px;
  overflow: hidden;
  opacity: 0;
  transform: translateY(40px);
  transition: all 0.8s var(--ease-out-expo);
}

.project-card.is-visible {
  opacity: 1;
  transform: translateY(0);
}

.project-card:hover {
  border-color: var(--color-accent-dim);
}

.project-card:hover .project-placeholder {
  background: var(--color-accent);
}

.project-card:hover .placeholder-number {
  color: var(--color-bg);
}

/* Project Image */
.project-image {
  aspect-ratio: 16 / 9;
  overflow: hidden;
  background: var(--color-bg);
  display: flex;
  align-items: center;
  justify-content: center;
}

.project-img {
  width: 100%;
  height: 100%;
  object-fit: contain;
  padding: 0.5rem;
  transition: transform 0.5s ease, filter 0.5s ease;
  filter: grayscale(20%) brightness(0.9);
}

.project-card:hover .project-img {
  transform: scale(1.05);
  filter: grayscale(0%) brightness(1);
}

.project-placeholder {
  width: 100%;
  height: 100%;
  background: var(--color-bg);
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background 0.5s ease;
}

.placeholder-number {
  font-family: var(--font-display);
  font-size: 3rem;
  font-weight: 300;
  color: var(--color-text-muted);
  transition: color 0.5s ease;
}

/* Project Content */
.project-content {
  padding: 1.75rem;
}

.project-category {
  display: inline-block;
  font-size: 0.7rem;
  font-weight: 400;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--color-accent-dim);
  margin-bottom: 0.75rem;
}

.project-title {
  font-family: var(--font-display);
  font-size: 1.5rem;
  font-weight: 400;
  color: var(--color-text);
  margin-bottom: 0.75rem;
}

.project-description {
  font-size: 0.9rem;
  font-weight: 300;
  line-height: 1.7;
  color: var(--color-text-secondary);
  margin-bottom: 1rem;
}

.project-highlights {
  list-style: none;
  padding: 0;
  margin: 0 0 1.25rem 0;
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
}

.project-highlights li {
  font-size: 0.8rem;
  font-weight: 300;
  line-height: 1.5;
  color: var(--color-text-muted);
  padding-left: 1rem;
  position: relative;
}

.project-highlights li::before {
  content: '→';
  position: absolute;
  left: 0;
  color: var(--color-accent-dim);
  font-size: 0.7rem;
}

/* Tags */
.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.tag {
  font-size: 0.75rem;
  font-weight: 300;
  padding: 0.35rem 0.75rem;
  background: var(--color-bg);
  border: 1px solid var(--color-border);
  border-radius: 2px;
  color: var(--color-text-muted);
}

/* Project Link */
.project-link {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.85rem;
  font-weight: 300;
  color: var(--color-text);
  transition: color 0.3s ease;
}

.project-link:hover {
  color: var(--color-accent);
  opacity: 1;
}

.project-link svg {
  transition: transform 0.3s ease;
}

.project-link:hover svg {
  transform: translate(3px, -3px);
}

.project-private {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.8rem;
  font-weight: 300;
  color: var(--color-text-muted);
}

.project-footer {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.project-note {
  font-size: 0.8rem;
  font-weight: 300;
  font-style: italic;
  color: var(--color-text-muted);
  line-height: 1.5;
  padding-left: 0.5rem;
  border-left: 2px solid var(--color-accent-dim);
}

/* Responsive */
@media (max-width: 768px) {
  .portfolio {
    padding: 6rem 2rem;
  }

  .projects-grid {
    grid-template-columns: 1fr;
  }
}
</style>

