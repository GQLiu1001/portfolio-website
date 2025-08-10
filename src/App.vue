<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'
import HomeView from './views/HomeView.vue'
import AboutView from './views/AboutView.vue'
import ProjectsView from './views/ProjectsView.vue'

const sections = [
  { id: 'home', name: 'Home', component: HomeView },
  { id: 'about', name: 'About', component: AboutView },
  { id: 'projects', name: 'Projects', component: ProjectsView }
]

const activeSection = ref('home')
const scrollBlur = ref(0)
const scrollY = ref(0)

const darkMode = ref(false)
const toggleDarkMode = () => {
  darkMode.value = !darkMode.value
}

const scrollToSection = (sectionId: string): void => {
  const element = document.getElementById(sectionId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}

const handleScroll = (): void => {
  scrollY.value = window.scrollY
  // 计算模糊效果值，最大值为10px
  scrollBlur.value = Math.min(10, scrollY.value / 100)
  checkActiveSection()
}

const checkActiveSection = (): void => {
  const scrollPosition = scrollY.value + 100 // 添加偏移量以提前激活

  for (const section of sections) {
    const element = document.getElementById(section.id)
    if (element) {
      const offsetTop = element.offsetTop
      const offsetBottom = offsetTop + element.offsetHeight

      if (scrollPosition >= offsetTop && scrollPosition < offsetBottom) {
        activeSection.value = section.id
        break
      }
    }
  }
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  handleScroll() // 初始检查
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <div :class="{ 'dark': darkMode }">
    <div class="app-container">
      <header class="header">
        <nav class="nav">
          <div class="nav-links">
            <a 
              v-for="section in sections" 
              :key="section.id"
              :class="['nav-link', { 'active': activeSection === section.id }]"
              @click.prevent="scrollToSection(section.id)"
              href="#"
            >
              {{ section.name }}
            </a>
          </div>
        </nav>
      </header>

      <main class="main-content">
        <section 
          v-for="(section, index) in sections" 
          :key="section.id" 
          :id="section.id" 
          class="page-section"
          :style="{ 
            filter: activeSection !== section.id && index < sections.findIndex(s => s.id === activeSection)
              ? `blur(${scrollBlur}px)` 
              : 'none',
            opacity: activeSection !== section.id && index < sections.findIndex(s => s.id === activeSection)
              ? Math.max(0.3, 1 - scrollBlur/10)
              : 1
          }"
        >
          <component :is="section.component" />
        </section>
      </main>


    </div>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap');

* {
  font-family: 'Inter', sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  scroll-behavior: smooth;
}

body {
  overflow-x: hidden;
}

.app-container {
  min-height: 100vh;
  background: linear-gradient(135deg, #e6f0ff 0%, #f8e6ff 100%);
  color: #111;
  position: relative;
}

.dark .app-container {
  background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
  color: #fff;
}

.header {
  padding: 1.5rem 0;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
}

.nav {
  display: flex;
  justify-content: center;
  max-width: 500px;
  margin: 0 auto;
  background-color: rgba(255, 255, 255, 0.2);
  backdrop-filter: blur(8px);
  border-radius: 50px;
  padding: 0.75rem 2rem;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.05);
  transition: background-color 0.3s;
}

.nav:hover {
  background-color: rgba(255, 255, 255, 0.4);
}

.dark .nav {
  background-color: rgba(30, 30, 50, 0.2);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
}

.dark .nav:hover {
  background-color: rgba(30, 30, 50, 0.4);
}

.nav-links {
  display: flex;
  gap: 2rem;
}

.nav-link {
  text-decoration: none;
  color: #333;
  font-weight: 600;
  position: relative;
  padding: 0.25rem 0;
  cursor: pointer;
  transition: color 0.3s;
  text-shadow: 0 1px 2px rgba(255, 255, 255, 0.2);
}

.dark .nav-link {
  color: #eee;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.3);
}

.nav-link:hover {
  color: #000;
}

.dark .nav-link:hover {
  color: #fff;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: -2px;
  left: 50%;
  width: 0;
  height: 2px;
  background-color: currentColor;
  border-radius: 2px;
  opacity: 0;
  transform: translateX(-50%);
  transition: width 0.3s ease, opacity 0.3s ease;
}

.nav-link.active {
  font-weight: 700;
  color: #000;
}

.dark .nav-link.active {
  color: #fff;
}

.nav-link.active::after {
  width: 100%;
  opacity: 1;
}

.main-content {
  padding-top: 80px; /* 为固定导航条留出空间 */
}

.page-section {
  min-height: 100vh;
  width: 100%;
  transition: filter 0.4s ease, opacity 0.4s ease, transform 0.4s ease;
  will-change: filter, opacity, transform;
}

@media (max-width: 768px) {
  .nav {
    padding: 0.5rem 1rem;
    border-radius: 30px;
    max-width: 90%;
  }
  
  .nav-links {
    gap: 1rem;
    font-size: 0.85rem;
  }
}
</style>
