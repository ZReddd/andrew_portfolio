<script setup>
import { ref, onMounted } from 'vue'

const isVisible = ref(false)
const sectionRef = ref(null)

const skillCategories = [
  {
    name: 'Languages',
    skills: [
      { name: 'JavaScript', icon: 'js' },
      { name: 'TypeScript', icon: 'ts' },
      { name: 'PHP', icon: 'php' },
      { name: 'C++', icon: 'cpp' },
      { name: 'HTML', icon: 'html' },
      { name: 'CSS', icon: 'css' }
    ]
  },
  {
    name: 'Frontend',
    skills: [
      { name: 'Vue.js', icon: 'vue' },
      { name: 'React', icon: 'react' },
      { name: 'Vuetify', icon: 'vuetify' }
    ]
  },
  {
    name: 'Backend',
    skills: [
      { name: 'Laravel', icon: 'laravel' },
      { name: 'Node.js', icon: 'node' },
      { name: 'Express', icon: 'express' },
      { name: 'REST APIs', icon: 'api' }
    ]
  },
  {
    name: 'Database',
    skills: [
      { name: 'MySQL', icon: 'mysql' },
      { name: 'MongoDB', icon: 'mongodb' },
      { name: 'Power BI', icon: 'powerbi' }
    ]
  },
  {
    name: 'DevOps & Cloud',
    skills: [
      { name: 'AWS', icon: 'aws' },
      { name: 'GCP', icon: 'gcp' },
      { name: 'Docker', icon: 'docker' },
      { name: 'Git', icon: 'git' }
    ]
  },
  {
    name: 'Tools',
    skills: [
      { name: 'Figma', icon: 'figma' },
      { name: 'Jira', icon: 'jira' },
      { name: 'WordPress', icon: 'wordpress' },
      { name: 'Cursor', icon: 'cursor' }
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
    { threshold: 0.1 }
  )

  if (sectionRef.value) {
    observer.observe(sectionRef.value)
  }
})
</script>

<template>
  <section id="skills" class="skills" ref="sectionRef">
    <div class="skills-container">
      <div class="section-header" :class="{ 'is-visible': isVisible }">
        <span class="section-number">04</span>
        <div class="section-title-wrapper">
          <h2 class="section-title">Skills & Tools</h2>
          <span class="section-subtitle">Technologies I work with</span>
        </div>
        <div class="section-line"></div>
      </div>

      <div class="skills-grid">
        <div 
          v-for="(category, catIndex) in skillCategories" 
          :key="category.name"
          class="skill-category"
          :class="{ 'is-visible': isVisible }"
          :style="{ transitionDelay: `${0.1 + catIndex * 0.1}s` }"
        >
          <h3 class="category-name">{{ category.name }}</h3>
          <div class="category-skills">
            <div 
              v-for="(skill, skillIndex) in category.skills" 
              :key="skill.name"
              class="skill-item"
              :style="{ animationDelay: `${0.3 + catIndex * 0.1 + skillIndex * 0.05}s` }"
            >
              <div class="skill-icon" :class="`icon-${skill.icon}`">
                <component :is="getIcon(skill.icon)" />
              </div>
              <span class="skill-name">{{ skill.name }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  methods: {
    getIcon(icon) {
      // Return a simple div, we'll use CSS for icons
      return 'div'
    }
  }
}
</script>

<style scoped>
.skills {
  padding: 8rem 4rem;
  background: var(--color-bg-secondary);
  position: relative;
}

.skills::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 1px;
  background: var(--color-border);
}

.skills-container {
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

/* Skills Grid */
.skills-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 3rem 4rem;
}

.skill-category {
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s var(--ease-out-expo);
}

.skill-category.is-visible {
  opacity: 1;
  transform: translateY(0);
}

.category-name {
  font-size: 0.75rem;
  font-weight: 400;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--color-accent);
  margin-bottom: 1.25rem;
  padding-bottom: 0.75rem;
  border-bottom: 1px solid var(--color-border);
}

.category-skills {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
}

.skill-item {
  display: flex;
  align-items: center;
  gap: 0.6rem;
  padding: 0.5rem 0.9rem;
  background: var(--color-bg);
  border: 1px solid var(--color-border);
  border-radius: 4px;
  cursor: default;
  transition: all 0.3s ease;
  animation: skillFadeIn 0.5s ease forwards;
  opacity: 0;
}

@keyframes skillFadeIn {
  from {
    opacity: 0;
    transform: translateY(10px) scale(0.95);
  }
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

.skill-item:hover {
  border-color: var(--color-accent);
  transform: translateY(-2px);
  box-shadow: 0 4px 20px rgba(201, 166, 107, 0.1);
}

.skill-item:hover .skill-icon {
  transform: scale(1.1) rotate(5deg);
}

.skill-icon {
  width: 18px;
  height: 18px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: transform 0.3s ease;
}

/* Icon Colors */
.skill-icon::before {
  content: '';
  width: 100%;
  height: 100%;
  border-radius: 3px;
  transition: all 0.3s ease;
}

.icon-js::before { background: #f7df1e; }
.icon-ts::before { background: #3178c6; }
.icon-php::before { background: #777bb4; }
.icon-cpp::before { background: #00599c; }
.icon-html::before { background: #e34f26; }
.icon-css::before { background: #1572b6; }
.icon-vue::before { background: #4fc08d; }
.icon-react::before { background: #61dafb; }
.icon-vuetify::before { background: #1867c0; }
.icon-laravel::before { background: #ff2d20; }
.icon-node::before { background: #339933; }
.icon-express::before { background: #ffffff; }
.icon-api::before { background: var(--color-accent); }
.icon-mysql::before { background: #4479a1; }
.icon-mongodb::before { background: #47a248; }
.icon-powerbi::before { background: #f2c811; }
.icon-aws::before { background: #ff9900; }
.icon-gcp::before { background: #4285f4; }
.icon-docker::before { background: #2496ed; }
.icon-git::before { background: #f05032; }
.icon-figma::before { background: #f24e1e; }
.icon-jira::before { background: #0052cc; }
.icon-wordpress::before { background: #21759b; }
.icon-cursor::before { background: linear-gradient(135deg, #7c3aed, #2563eb); }

.skill-name {
  font-size: 0.8rem;
  font-weight: 400;
  color: var(--color-text-secondary);
  white-space: nowrap;
}

.skill-item:hover .skill-name {
  color: var(--color-text);
}

/* Responsive */
@media (max-width: 900px) {
  .skills {
    padding: 6rem 2rem;
  }

  .skills-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 2rem;
  }
}

@media (max-width: 600px) {
  .skills-grid {
    grid-template-columns: 1fr;
  }
}
</style>

