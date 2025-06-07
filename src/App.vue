<script setup>
import { onMounted, ref } from 'vue'
import Header from "./parts/header.vue"
import Hero from "./parts/hero.vue"
// import Footer from "./parts/footer.vue"

// État global de l'application
const isLoading = ref(true)
const theme = ref('light')

// Gestion du thème
const toggleTheme = () => {
  theme.value = theme.value === 'light' ? 'dark' : 'light'
  document.documentElement.setAttribute('data-theme', theme.value)
}

// Initialisation
onMounted(() => {
  // Détection du thème système
  const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches
  theme.value = prefersDark ? 'dark' : 'light'
  document.documentElement.setAttribute('data-theme', theme.value)

  // Simulation de chargement
  setTimeout(() => {
    isLoading.value = false
  }, 1000)
})
</script>

<template>
  <div id="app" :class="{ 'loading': isLoading }">
    <!-- Indicateur de chargement -->
    <Transition name="fade">
      <div v-if="isLoading" class="loading-screen">
        <div class="spinner"></div>
        <p>Chargement...</p>
      </div>
    </Transition>
  
    <!-- Contenu principal -->
    <Transition name="slide-up" appear>
      <div v-if="!isLoading" class="app-content">
        <header class="app-header">
          <Header @toggle-theme="toggleTheme" :current-theme="theme" />
        </header>
  
        <main class="app-main">
          <Hero />
  
          <!-- Section pour du contenu additionnel -->
          <section class="content-section">
            <slot name="additional-content">
              <!-- Contenu par défaut ou slot pour d'autres composants -->
            </slot>
          </section>
        </main>
  
        <footer class="app-footer">
          <Footer />
        </footer>
      </div>
    </Transition>
  </div>
</template>

<style scoped>
/* Variables CSS pour les thèmes */
:root {
  --primary-color: #3b82f6;
  --background-color: #ffffff;
  --text-color: #1f2937;
  --border-color: #e5e7eb;
}

[data-theme="dark"] {
  --primary-color: #60a5fa;
  --background-color: #111827;
  --text-color: #f9fafb;
  --border-color: #374151;
}

#app {
  min-height: 100vh;
  background-color: var(--background-color);
  color: var(--text-color);
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  transition: background-color 0.3s ease, color 0.3s ease;
}

.loading-screen {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: var(--background-color);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  z-index: 9999;
}

.spinner {
  width: 40px;
  height: 40px;
  border: 3px solid var(--border-color);
  border-top: 3px solid var(--primary-color);
  border-radius: 50%;
  animation: spin 1s linear infinite;
  margin-bottom: 1rem;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(360deg);
  }
}

.app-content {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.app-header {
  position: sticky;
  top: 0;
  z-index: 100;
  backdrop-filter: blur(10px);
  border-bottom: 1px solid var(--border-color);
}

.app-main {
  flex: 1;
  display: flex;
  flex-direction: column;
}

.content-section {
  padding: 2rem 1rem;
  max-width: 1200px;
  margin: 0 auto;
  width: 100%;
}

.app-footer {
  margin-top: auto;
  border-top: 1px solid var(--border-color);
}

/* Animations de transition */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.slide-up-enter-active {
  transition: all 0.6s ease;
}

.slide-up-enter-from {
  opacity: 0;
  transform: translateY(30px);
}

/* Responsive design */
@media (max-width: 768px) {
  .content-section {
    padding: 1rem 0.5rem;
  }
}

/* Accessibilité */
@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}

/* Amélioration du focus pour l'accessibilité */
:focus-visible {
  outline: 2px solid var(--primary-color);
  outline-offset: 2px;
}
</style>