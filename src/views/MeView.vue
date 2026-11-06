<script setup lang="ts">
import { ref } from 'vue'
import { RouterLink } from 'vue-router'

const copiedField = ref<string | null>(null)

async function copyValue(text: string, fieldName: string) {
  try {
    await navigator.clipboard.writeText(text)
    copiedField.value = fieldName
    setTimeout(() => {
      if (copiedField.value === fieldName) {
        copiedField.value = null
      }
    }, 2000)
  } catch {
    copiedField.value = null
  }
}
</script>

<template>
  <div class="page-wrapper">
    <div class="container">
      <header class="top-nav">
        <RouterLink to="/" class="nav-back-btn">
          <svg viewBox="0 0 24 24" width="16" height="16" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <line x1="19" y1="12" x2="5" y2="12"></line>
            <polyline points="12 19 5 12 12 5"></polyline>
          </svg>
          Back to Home
        </RouterLink>
      </header>

      <main class="vcard-card">
        <section class="profile-hero">
          <div class="avatar-container">
            <div class="avatar-frame">
              <span class="avatar-monogram">DR</span>
            </div>
            <div class="status-badge" title="Open to opportunities">
              <span class="status-dot"></span>
              <span>Open to work</span>
            </div>
          </div>

          <div class="profile-meta">
            <h1 class="person-name">Daniil Radzevich</h1>
            <p class="person-alias">@hita_u &bull; hita</p>
            <div class="role-tag">Fullstack Developer</div>
            <p class="summary-text">
              18-year-old software developer from Mogilev, Belarus. Passionate about building reliable web applications, responsive user interfaces, backend services, and interactive projects.
            </p>
          </div>
        </section>

        <section class="section-block">
          <h2 class="section-title">
            <svg viewBox="0 0 24 24" width="18" height="18" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"></path>
            </svg>
            Contacts &amp; Links
          </h2>

          <div class="contacts-grid">
            <div class="contact-card primary-contact">
              <div class="contact-info">
                <div class="contact-header">
                  <span class="contact-icon-wrapper">
                    <svg viewBox="0 0 24 24" width="18" height="18" fill="currentColor">
                      <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm4.64 6.8c-.15 1.58-.8 5.42-1.13 7.19-.14.75-.42 1-.68 1.03-.58.05-1.02-.38-1.58-.75-.88-.58-1.38-.94-2.23-1.5-.99-.65-.35-1.01.22-1.59.15-.15 2.71-2.48 2.76-2.69a.2.2 0 00-.05-.18c-.06-.05-.14-.03-.21-.02-.09.02-1.49.95-4.22 2.79-.4.27-.76.41-1.08.4-.36-.01-1.04-.2-1.55-.37-.63-.2-1.12-.31-1.08-.66.02-.18.27-.36.74-.55 2.92-1.27 4.86-2.11 5.83-2.51 2.78-1.16 3.35-1.36 3.73-1.36.08 0 .27.02.39.12.1.08.13.19.14.27-.01.06.01.24 0 .38z"/>
                    </svg>
                  </span>
                  <span class="contact-title">Telegram</span>
                  <span class="highlight-badge">Preferred</span>
                </div>
                <a href="https://t.me/hita_u" target="_blank" rel="noopener noreferrer" class="contact-val">@hita_u</a>
              </div>
              <button
                type="button"
                class="copy-btn"
                :class="{ active: copiedField === 'telegram' }"
                @click="copyValue('@hita_u', 'telegram')"
                aria-label="Copy Telegram username"
              >
                <span v-if="copiedField === 'telegram'">Copied!</span>
                <span v-else>Copy</span>
              </button>
            </div>

            <div class="contact-card">
              <div class="contact-info">
                <div class="contact-header">
                  <span class="contact-icon-wrapper">
                    <svg viewBox="0 0 24 24" width="18" height="18" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                      <path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"></path>
                    </svg>
                  </span>
                  <span class="contact-title">Phone</span>
                </div>
                <a href="tel:+375292181046" class="contact-val">+375 (29) 218-10-46</a>
              </div>
              <button
                type="button"
                class="copy-btn"
                :class="{ active: copiedField === 'phone' }"
                @click="copyValue('+375292181046', 'phone')"
                aria-label="Copy Phone number"
              >
                <span v-if="copiedField === 'phone'">Copied!</span>
                <span v-else>Copy</span>
              </button>
            </div>

            <div class="contact-card">
              <div class="contact-info">
                <div class="contact-header">
                  <span class="contact-icon-wrapper">
                    <svg viewBox="0 0 24 24" width="18" height="18" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                      <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"></path>
                      <polyline points="22,6 12,13 2,6"></polyline>
                    </svg>
                  </span>
                  <span class="contact-title">Email</span>
                </div>
                <a href="mailto:ninedefix@proton.me" class="contact-val">ninedefix@proton.me</a>
              </div>
              <button
                type="button"
                class="copy-btn"
                :class="{ active: copiedField === 'email' }"
                @click="copyValue('ninedefix@proton.me', 'email')"
                aria-label="Copy Email address"
              >
                <span v-if="copiedField === 'email'">Copied!</span>
                <span v-else>Copy</span>
              </button>
            </div>

            <div class="contact-card">
              <div class="contact-info">
                <div class="contact-header">
                  <span class="contact-icon-wrapper">
                    <svg viewBox="0 0 24 24" width="18" height="18" fill="currentColor">
                      <path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"/>
                    </svg>
                  </span>
                  <span class="contact-title">GitHub</span>
                </div>
                <a href="https://github.com/NotiLo-A" target="_blank" rel="noopener noreferrer" class="contact-val">NotiLo-A</a>
              </div>
              <a href="https://github.com/NotiLo-A" target="_blank" rel="noopener noreferrer" class="copy-btn link-action">Visit</a>
            </div>
          </div>
        </section>

        <section class="section-block">
          <h2 class="section-title">
            <svg viewBox="0 0 24 24" width="18" height="18" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <rect x="2" y="7" width="20" height="14" rx="2" ry="2"></rect>
              <path d="M16 21V5a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v16"></path>
            </svg>
            Work &amp; Availability
          </h2>

          <div class="info-grid">
            <div class="info-item">
              <span class="info-label">Desired Role</span>
              <span class="info-value">Fullstack Developer</span>
            </div>
            <div class="info-item">
              <span class="info-label">Employment Type</span>
              <span class="info-value">Full-time, Part-time, Project, Internship</span>
            </div>
            <div class="info-item">
              <span class="info-label">Work Format</span>
              <span class="info-value">Remote, Hybrid, On-site</span>
            </div>
            <div class="info-item">
              <span class="info-label">Location</span>
              <span class="info-value">Mogilev, Belarus</span>
            </div>
            <div class="info-item">
              <span class="info-label">Citizenship</span>
              <span class="info-value">Belarus (Work permit: Belarus)</span>
            </div>
            <div class="info-item">
              <span class="info-label">Relocation &amp; Travel</span>
              <span class="info-value">Not relocating, open to business trips</span>
            </div>
          </div>
        </section>

        <section class="section-block">
          <h2 class="section-title">
            <svg viewBox="0 0 24 24" width="18" height="18" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <polyline points="16 18 22 12 16 6"></polyline>
              <polyline points="8 6 2 12 8 18"></polyline>
            </svg>
            Skills &amp; Technologies
          </h2>

          <div class="skills-groups">
            <div class="skill-category">
              <span class="category-name">Frontend</span>
              <div class="tags-list">
                <span class="tag">Vue 3</span>
                <span class="tag">TypeScript</span>
                <span class="tag">JavaScript</span>
                <span class="tag">React</span>
                <span class="tag">HTML5 / CSS</span>
              </div>
            </div>

            <div class="skill-category">
              <span class="category-name">Backend &amp; Database</span>
              <div class="tags-list">
                <span class="tag">Node.js</span>
                <span class="tag">Python</span>
                <span class="tag">SQL</span>
                <span class="tag">SOLID</span>
                <span class="tag">SaaS Architecture</span>
              </div>
            </div>

            <div class="skill-category">
              <span class="category-name">DevOps &amp; Infrastructure</span>
              <div class="tags-list">
                <span class="tag">Docker</span>
                <span class="tag">Docker Compose</span>
                <span class="tag">CI/CD</span>
                <span class="tag">Git</span>
                <span class="tag">GitHub</span>
                <span class="tag">GitLab</span>
                <span class="tag">Linux</span>
              </div>
            </div>

            <div class="skill-category">
              <span class="category-name">Mobile &amp; Creative</span>
              <div class="tags-list">
                <span class="tag">Android</span>
                <span class="tag">Kotlin</span>
                <span class="tag">Blender 3D</span>
                <span class="tag">Arduino</span>
              </div>
            </div>
          </div>
        </section>

        <section class="section-block">
          <h2 class="section-title">
            <svg viewBox="0 0 24 24" width="18" height="18" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M22 10v6M2 10l10-5 10 5-10 5z"></path>
              <path d="M6 12v5c3 3 9 3 12 0v-5"></path>
            </svg>
            Education
          </h2>

          <div class="education-card">
            <div class="edu-header">
              <div class="edu-title-group">
                <h3 class="edu-school">Mogilev State Polytechnic College (MGPK)</h3>
                <p class="edu-major">Software Development and Maintenance</p>
              </div>
              <span class="edu-badge">Expected 2027</span>
            </div>
            <p class="edu-level">Vocational / Specialized Secondary Education</p>
          </div>
        </section>

        <section class="section-block">
          <h2 class="section-title">
            <svg viewBox="0 0 24 24" width="18" height="18" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <circle cx="12" cy="12" r="10"></circle>
              <line x1="2" y1="12" x2="22" y2="12"></line>
              <path d="M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"></path>
            </svg>
            Languages
          </h2>

          <div class="languages-grid">
            <div class="language-card">
              <div class="lang-top">
                <span class="lang-name">Russian</span>
                <span class="lang-level-badge">Native</span>
              </div>
              <div class="lang-bar">
                <div class="lang-progress" style="width: 100%;"></div>
              </div>
            </div>

            <div class="language-card">
              <div class="lang-top">
                <span class="lang-name">Belarusian</span>
                <span class="lang-level-badge">C1 &bull; Advanced</span>
              </div>
              <div class="lang-bar">
                <div class="lang-progress" style="width: 85%;"></div>
              </div>
            </div>

            <div class="language-card">
              <div class="lang-top">
                <span class="lang-name">English</span>
                <span class="lang-level-badge">B1 &bull; Intermediate</span>
              </div>
              <div class="lang-bar">
                <div class="lang-progress" style="width: 60%;"></div>
              </div>
            </div>

            <div class="language-card">
              <div class="lang-top">
                <span class="lang-name">Polish</span>
                <span class="lang-level-badge">A2 &bull; Elementary</span>
              </div>
              <div class="lang-bar">
                <div class="lang-progress" style="width: 35%;"></div>
              </div>
            </div>
          </div>
        </section>

        <footer class="card-footer">
          <RouterLink to="/" class="footer-back-link">
            &larr; Back to Main Page
          </RouterLink>
          <span class="footer-copy">Daniil Radzevich &bull; hita.gay</span>
        </footer>
      </main>
    </div>
  </div>
</template>

<style scoped>
.page-wrapper {
  min-height: 100vh;
  padding: 2rem 1rem 3rem;
  background-color: var(--bg);
  background-image:
    radial-gradient(circle at 10% 20%, var(--accent-bg) 0%, transparent 40%),
    radial-gradient(circle at 90% 80%, var(--accent-bg) 0%, transparent 40%);
  display: flex;
  justify-content: center;
  align-items: flex-start;
}

.container {
  width: 100%;
  max-width: 720px;
}

.top-nav {
  margin-bottom: 1.25rem;
}

.nav-back-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.5rem 1rem;
  font-size: 0.9rem;
  font-weight: 500;
  color: var(--text-muted);
  background: var(--card-bg);
  border: 1px solid var(--border);
  border-radius: 9999px;
  text-decoration: none;
  backdrop-filter: blur(8px);
  transition: all 0.2s ease;
}

.nav-back-btn:hover {
  color: var(--text-h);
  border-color: var(--accent);
  transform: translateX(-2px);
}

.vcard-card {
  background: var(--card-bg);
  border: 1px solid var(--border);
  border-radius: 24px;
  box-shadow: var(--shadow);
  backdrop-filter: blur(12px);
  padding: 2.5rem 2rem;
  display: flex;
  flex-direction: column;
  gap: 2.25rem;
}

.profile-hero {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  gap: 1.25rem;
  padding-bottom: 2rem;
  border-bottom: 1px solid var(--border);
}

.avatar-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.75rem;
}

.avatar-frame {
  width: 96px;
  height: 96px;
  border-radius: 50%;
  background: linear-gradient(135deg, var(--accent) 0%, #ec4899 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 8px 20px -4px var(--accent-bg);
  border: 3px solid var(--border);
}

.avatar-monogram {
  font-size: 2.25rem;
  font-weight: 800;
  color: #ffffff;
  letter-spacing: -1px;
}

.status-badge {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.3rem 0.8rem;
  background: rgba(16, 185, 129, 0.1);
  border: 1px solid rgba(16, 185, 129, 0.25);
  border-radius: 9999px;
  font-size: 0.8rem;
  font-weight: 600;
  color: #10b981;
}

.status-dot {
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background-color: #10b981;
  box-shadow: 0 0 6px #10b981;
}

.person-name {
  font-size: 2.25rem;
  font-weight: 800;
  color: var(--text-h);
  margin: 0;
  letter-spacing: -0.02em;
}

.person-alias {
  font-size: 0.95rem;
  color: var(--text-muted);
  margin: 0.25rem 0 0.75rem;
  font-weight: 500;
}

.role-tag {
  display: inline-block;
  padding: 0.35rem 1rem;
  border-radius: 9999px;
  background: var(--accent-bg);
  color: var(--accent);
  font-weight: 600;
  font-size: 0.95rem;
  margin-bottom: 0.75rem;
  border: 1px solid var(--accent-bg);
}

.summary-text {
  max-width: 520px;
  margin: 0 auto;
  font-size: 0.95rem;
  line-height: 1.6;
  color: var(--text-muted);
}

.section-block {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.section-title {
  display: flex;
  align-items: center;
  gap: 0.6rem;
  font-size: 1.15rem;
  font-weight: 700;
  color: var(--text-h);
  margin: 0;
}

.contacts-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 0.75rem;
}

.contact-card {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.9rem 1.1rem;
  background: var(--subtle-bg);
  border: 1px solid var(--border);
  border-radius: 14px;
  transition: all 0.2s ease;
}

.contact-card:hover {
  border-color: var(--accent);
  background: var(--accent-bg);
}

.primary-contact {
  border-color: rgba(147, 51, 234, 0.3);
}

.contact-info {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
  min-width: 0;
}

.contact-header {
  display: flex;
  align-items: center;
  gap: 0.45rem;
}

.contact-icon-wrapper {
  color: var(--accent);
  display: flex;
  align-items: center;
}

.contact-title {
  font-size: 0.75rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: var(--text-muted);
}

.highlight-badge {
  font-size: 0.65rem;
  font-weight: 700;
  padding: 0.15rem 0.45rem;
  background: var(--accent);
  color: #ffffff;
  border-radius: 9999px;
  line-height: 1;
}

.contact-val {
  font-size: 0.95rem;
  font-weight: 600;
  color: var(--text-h);
  text-decoration: none;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.contact-val:hover {
  color: var(--accent);
}

.copy-btn {
  background: var(--card-bg);
  border: 1px solid var(--border);
  color: var(--text);
  font-size: 0.75rem;
  font-weight: 600;
  padding: 0.35rem 0.75rem;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.15s ease;
  white-space: nowrap;
  flex-shrink: 0;
}

.copy-btn:hover {
  background: var(--border);
  color: var(--text-h);
}

.copy-btn.active {
  background: #10b981;
  color: #ffffff;
  border-color: #10b981;
}

.link-action {
  text-decoration: none;
}

.info-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 0.75rem;
}

.info-item {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
  padding: 0.85rem 1rem;
  background: var(--subtle-bg);
  border: 1px solid var(--border);
  border-radius: 12px;
}

.info-label {
  font-size: 0.75rem;
  font-weight: 600;
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 0.04em;
}

.info-value {
  font-size: 0.95rem;
  font-weight: 600;
  color: var(--text-h);
}

.skills-groups {
  display: flex;
  flex-direction: column;
  gap: 0.85rem;
}

.skill-category {
  display: flex;
  flex-direction: column;
  gap: 0.45rem;
}

.category-name {
  font-size: 0.8rem;
  font-weight: 600;
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 0.04em;
}

.tags-list {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.tag {
  display: inline-flex;
  align-items: center;
  padding: 0.35rem 0.75rem;
  background: var(--subtle-bg);
  border: 1px solid var(--border);
  border-radius: 8px;
  font-size: 0.85rem;
  font-weight: 500;
  color: var(--text-h);
  transition: all 0.15s ease;
}

.tag:hover {
  border-color: var(--accent);
  background: var(--accent-bg);
  color: var(--accent);
}

.education-card {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  padding: 1.1rem 1.25rem;
  background: var(--subtle-bg);
  border: 1px solid var(--border);
  border-radius: 14px;
}

.edu-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 1rem;
  flex-wrap: wrap;
}

.edu-title-group {
  display: flex;
  flex-direction: column;
  gap: 0.2rem;
}

.edu-school {
  font-size: 1.05rem;
  font-weight: 700;
  color: var(--text-h);
  margin: 0;
}

.edu-major {
  font-size: 0.9rem;
  font-weight: 500;
  color: var(--accent);
  margin: 0;
}

.edu-badge {
  font-size: 0.75rem;
  font-weight: 700;
  padding: 0.25rem 0.6rem;
  border-radius: 9999px;
  background: var(--accent-bg);
  color: var(--accent);
  border: 1px solid var(--border);
  white-space: nowrap;
}

.edu-level {
  font-size: 0.8rem;
  color: var(--text-muted);
  margin: 0;
}

.languages-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 0.75rem;
}

.language-card {
  padding: 0.9rem 1rem;
  background: var(--subtle-bg);
  border: 1px solid var(--border);
  border-radius: 12px;
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
}

.lang-top {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.lang-name {
  font-size: 0.95rem;
  font-weight: 600;
  color: var(--text-h);
}

.lang-level-badge {
  font-size: 0.75rem;
  font-weight: 600;
  color: var(--text-muted);
}

.lang-bar {
  height: 6px;
  background: var(--border);
  border-radius: 9999px;
  overflow: hidden;
}

.lang-progress {
  height: 100%;
  background: linear-gradient(90deg, var(--accent) 0%, #ec4899 100%);
  border-radius: 9999px;
}

.card-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 1.5rem;
  border-top: 1px solid var(--border);
  font-size: 0.85rem;
  color: var(--text-muted);
  flex-wrap: wrap;
  gap: 1rem;
}

.footer-back-link {
  color: var(--accent);
  text-decoration: none;
  font-weight: 600;
  transition: all 0.15s ease;
}

.footer-back-link:hover {
  text-decoration: underline;
}

.footer-copy {
  font-weight: 500;
}

@media (max-width: 640px) {
  .vcard-card {
    padding: 1.75rem 1.25rem;
    border-radius: 20px;
    gap: 1.75rem;
  }

  .person-name {
    font-size: 1.75rem;
  }

  .contacts-grid,
  .info-grid,
  .languages-grid {
    grid-template-columns: 1fr;
  }

  .card-footer {
    flex-direction: column;
    text-align: center;
    gap: 0.5rem;
  }
}
</style>
