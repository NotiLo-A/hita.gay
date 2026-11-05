<script setup lang="ts">
import { RouterLink } from 'vue-router'
</script>

<template>
  <div class="page-container">
    <div class="card profile-card">
      <div class="avatar-wrapper">
        <div class="avatar">✨</div>
      </div>

      <h1 class="name">hita</h1>
      <p class="tagline">Developer & Creator</p>

      <div class="bio">
        <p>
          Привет! Это страница-заглушка <strong>hita.gay/me</strong>.
        </p>
        <p>
          Здесь можно разместить информацию о себе, ссылки на социальные сети, проекты и контакты.
        </p>
      </div>

      <div class="links-section">
        <div class="link-item">
          <span class="link-label">Сайт:</span>
          <a href="https://hita.gay" class="link-url">hita.gay</a>
        </div>
        <div class="link-item">
          <span class="link-label">Статус:</span>
          <span class="status-indicator">
            <span class="dot"></span> Online
          </span>
        </div>
      </div>

      <div class="actions">
        <RouterLink to="/" class="btn btn-secondary">
          &larr; На главную
        </RouterLink>
      </div>
    </div>
  </div>
</template>

<style scoped>
.page-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: calc(80vh - 100px);
  padding: 1.5rem;
}

.profile-card {
  text-align: center;
  max-width: 540px;
  width: 100%;
  padding: 3rem 2rem;
  background: var(--card-bg);
  border: 1px solid var(--border);
  border-radius: 20px;
  box-shadow: var(--shadow);
  backdrop-filter: blur(8px);
}

.avatar-wrapper {
  margin-bottom: 1.25rem;
}

.avatar {
  width: 80px;
  height: 80px;
  margin: 0 auto;
  border-radius: 50%;
  background: linear-gradient(135deg, rgba(168, 85, 247, 0.2), rgba(236, 72, 153, 0.2));
  border: 2px solid var(--accent);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2.2rem;
}

.name {
  font-size: 2.2rem;
  font-weight: 800;
  margin: 0 0 0.25rem;
  color: var(--text-h);
}

.tagline {
  font-size: 1rem;
  color: var(--accent);
  font-weight: 500;
  margin-bottom: 1.5rem;
}

.bio {
  text-align: left;
  line-height: 1.6;
  color: var(--text-muted);
  background: var(--accent-bg);
  padding: 1.2rem;
  border-radius: 12px;
  margin-bottom: 1.75rem;
  border: 1px solid var(--border);
}

.bio p {
  margin: 0.5rem 0;
}

.bio p:first-child {
  margin-top: 0;
}

.bio p:last-child {
  margin-bottom: 0;
}

.links-section {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
  margin-bottom: 2rem;
  text-align: left;
}

.link-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.6rem 0.9rem;
  border-radius: 8px;
  background: var(--subtle-bg);
}

.link-label {
  font-weight: 500;
  font-size: 0.95rem;
}

.link-url {
  color: var(--accent);
  text-decoration: none;
  font-weight: 500;
}

.link-url:hover {
  text-decoration: underline;
}

.status-indicator {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  font-size: 0.9rem;
  color: #10b981;
  font-weight: 600;
}

.dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background-color: #10b981;
  box-shadow: 0 0 8px #10b981;
}

.actions {
  display: flex;
  justify-content: center;
}

.btn {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1.5rem;
  font-size: 1rem;
  font-weight: 600;
  border-radius: 12px;
  text-decoration: none;
  transition: all 0.2s ease;
}

.btn-secondary {
  background: var(--subtle-bg);
  color: var(--text-h);
  border: 1px solid var(--border);
}

.btn-secondary:hover {
  background: var(--border);
  transform: translateY(-2px);
}
</style>
