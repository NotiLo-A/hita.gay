<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <div class="app-layout">
    <header class="navbar">
      <div class="nav-container">
        <RouterLink to="/" class="brand">
          hita<span class="brand-accent">.gay</span>
        </RouterLink>
        <nav class="nav-links">
          <RouterLink to="/" class="nav-link" active-class="active" exact-active-class="active">Главная</RouterLink>
          <RouterLink to="/me" class="nav-link" active-class="active">Обо мне</RouterLink>
        </nav>
      </div>
    </header>

    <main class="main-content">
      <RouterView />
    </main>

    <footer class="footer">
      <p>&copy; {{ new Date().getFullYear() }} hita.gay &bull; All rights reserved.</p>
    </footer>
  </div>
</template>

<style scoped>
.app-layout {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.navbar {
  border-bottom: 1px solid var(--border);
  background: var(--nav-bg);
  backdrop-filter: blur(12px);
  position: sticky;
  top: 0;
  z-index: 50;
}

.nav-container {
  max-width: 1000px;
  margin: 0 auto;
  padding: 1rem 1.5rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.brand {
  font-size: 1.35rem;
  font-weight: 800;
  color: var(--text-h);
  text-decoration: none;
  letter-spacing: -0.02em;
}

.brand-accent {
  color: var(--accent);
}

.nav-links {
  display: flex;
  gap: 1rem;
}

.nav-link {
  text-decoration: none;
  font-weight: 500;
  font-size: 0.95rem;
  color: var(--text-muted);
  padding: 0.4rem 0.8rem;
  border-radius: 8px;
  transition: all 0.2s ease;
}

.nav-link:hover {
  color: var(--text-h);
  background: var(--subtle-bg);
}

.nav-link.active {
  color: var(--accent);
  background: var(--accent-bg);
}

.main-content {
  flex: 1;
}

.footer {
  text-align: center;
  padding: 1.5rem;
  color: var(--text-muted);
  font-size: 0.85rem;
  border-top: 1px solid var(--border);
}
</style>
