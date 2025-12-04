<script setup>
</script>

<template>
  <footer class="footer">
    <div class="footer-container">
      <div class="footer-content">
        <div class="footer-brand">
          <span class="footer-logo">Andrew Cheng</span>
          <p class="footer-tagline">Let's grab a coffee ☕ — I'd love to chat about the industry, collaborate on exciting projects, or brainstorm your next startup idea!</p>
        </div>
        
        <div class="footer-links">
          <a href="mailto:a88615123@gmail.com" class="footer-link">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <rect x="2" y="4" width="20" height="16" rx="2"/>
              <path d="M22 6L12 13L2 6"/>
            </svg>
            <span>Email</span>
          </a>
          <a href="https://www.linkedin.com/in/andrewcheng887/" target="_blank" class="footer-link">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor">
              <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
            </svg>
            <span>LinkedIn</span>
          </a>
          <a href="https://www.instagram.com/notandrewcheng" target="_blank" class="footer-link">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <rect x="2" y="2" width="20" height="20" rx="5"/>
              <circle cx="12" cy="12" r="4"/>
              <circle cx="18" cy="6" r="1.5" fill="currentColor" stroke="none"/>
            </svg>
            <span>Instagram</span>
          </a>
        </div>
      </div>
      
      <div class="footer-bottom">
        <span class="footer-copyright">© 2025 Andrew Cheng</span>
        <span class="footer-location">Adelaide, Australia</span>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  padding: 4rem 4rem 2rem;
  background: var(--color-bg);
  border-top: 1px solid var(--color-border);
}

.footer-container {
  max-width: 1200px;
  margin: 0 auto;
}

.footer-content {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 4rem;
}

.footer-brand {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.footer-logo {
  font-family: var(--font-display);
  font-size: 1.25rem;
  font-weight: 400;
  color: var(--color-text);
}

.footer-tagline {
  font-size: 0.9rem;
  font-weight: 300;
  color: var(--color-text-secondary);
  max-width: 400px;
  line-height: 1.6;
}

.footer-links {
  display: flex;
  gap: 2rem;
}

.footer-link {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.85rem;
  font-weight: 300;
  color: var(--color-text-secondary);
  transition: all 0.3s ease;
}

.footer-link svg {
  transition: transform 0.3s ease;
}

.footer-link:hover {
  color: var(--color-accent);
  opacity: 1;
}

.footer-link:hover svg {
  transform: translateY(-2px);
}

.footer-bottom {
  display: flex;
  justify-content: space-between;
  padding-top: 2rem;
  border-top: 1px solid var(--color-border);
}

.footer-copyright,
.footer-location {
  font-size: 0.8rem;
  font-weight: 300;
  color: var(--color-text-muted);
}

/* Responsive */
@media (max-width: 768px) {
  .footer {
    padding: 3rem 2rem 1.5rem;
  }

  .footer-content {
    flex-direction: column;
    gap: 2rem;
    margin-bottom: 2rem;
  }

  .footer-links {
    gap: 1.5rem;
  }

  .footer-bottom {
    flex-direction: column;
    gap: 0.5rem;
    align-items: center;
  }
}
</style>

