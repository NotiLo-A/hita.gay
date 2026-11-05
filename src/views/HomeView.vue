<script setup lang="ts">
import { RouterLink } from 'vue-router'
</script>

<template>
  <div class="page-container">
    <div class="card hero-card">
      <div class="badge">🚀 Under Construction</div>
      <h1 class="title">hita.gay</h1>
      <p class="subtitle">
        Сайт находится в разработке. Скоро здесь появится что-то интересное.
      </p>

      <div class="actions">
        <RouterLink to="/me" class="btn btn-primary">
          Обо мне / Me &rarr;
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

.hero-card {
  text-align: center;
  max-width: 580px;
  width: 100%;
  padding: 3rem 2rem;
  background: var(--card-bg);
  border: 1px solid var(--border);
  border-radius: 20px;
  box-shadow: var(--shadow);
  backdrop-filter: blur(8px);
}

.badge {
  display: inline-block;
  padding: 0.35rem 0.9rem;
  font-size: 0.85rem;
  font-weight: 600;
  color: var(--accent);
  background: var(--accent-bg);
  border: 1px solid var(--accent-border);
  border-radius: 9999px;
  margin-bottom: 1.5rem;
}

.title {
  font-size: 3rem;
  font-weight: 800;
  letter-spacing: -0.03em;
  margin: 0 0 1rem;
  background: linear-gradient(135deg, #a855f7 0%, #ec4899 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.subtitle {
  font-size: 1.15rem;
  line-height: 1.6;
  color: var(--text-muted);
  margin-bottom: 2rem;
}

.actions {
  display: flex;
  justify-content: center;
  gap: 1rem;
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

.btn-primary {
  background: var(--accent);
  color: #fff;
}

.btn-primary:hover {
  transform: translateY(-2px);
  filter: brightness(1.1);
}
</style>
