<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'
import wanbangImage from '../assets/image/wanbang.jpg'
import wanbangPhoneImage from '../assets/image/wanbang-phone.jpg'

// Projects view component
const projects = [
  {
    title: '链擎智仓 lqzc',
    description: '本项目基于真实线下店铺业务流程，利用 AI 赋能，系统由集成智能 AI 客服的线上商城、支持内部运营的仓储配送管理端以及配送司机服务端三大核心模块构成，实现了从线上下单到商品配送的全流程闭环。',
    image: wanbangImage,
    githubUrl: 'https://github.com/GQLiu1001/lqzc',
    demoUrl: 'https://www.wanbangflow.tech',
    tags: ['SPRINGBOOT', 'MYBATISPLUS', 'REDIS', 'RABBITMQ'],
    overlayImages: [
      wanbangPhoneImage,
      'https://pub-061d1fd03ea74e68849f186c401fde40.r2.dev/2025/08/861e4422a2a77d0ddd1009448818f569.png'
    ]
  },
  {
    title: '轻屿记 liteisle',
    description: '轻屿记是一款桌面端个人工作台，集沉浸式音乐、云同步笔记、专注模块、轻云盘于一体，以极简纯净的设计，打造专注高效的个人数字空间。',
    image: 'https://pub-061d1fd03ea74e68849f186c401fde40.r2.dev/2025/07/1c1e2d39827f528d53fe99170ec0850b.png',
    githubUrl: 'https://github.com/GQLiu1001/liteisle',
    demoUrl: '#',
    tags: ['SPRINGBOOT', 'MYBATISPLUS', 'REDIS', 'MINIO'],
    overlayImages: []
  }
]

// 项目卡片可见状态
const projectVisibility = ref(projects.map(() => false))

// 检查元素是否在视口内
const isElementInViewport = (el: HTMLElement): boolean => {
  const rect = el.getBoundingClientRect()
  return (
    rect.top <= (window.innerHeight * 0.8) &&
    rect.bottom >= (window.innerHeight * 0.2)
  )
}

// 更新动画状态
const updateAnimations = () => {
  const projectElements = document.querySelectorAll('.project-card')
  projectElements.forEach((el, index) => {
    projectVisibility.value[index] = isElementInViewport(el as HTMLElement)
  })
}

// 监听滚动事件
onMounted(() => {
  window.addEventListener('scroll', updateAnimations)
  updateAnimations() // 初始检查
})

onUnmounted(() => {
  window.removeEventListener('scroll', updateAnimations)
})
</script>

<template>
  <div class="projects-section">
    <h2 class="section-title">My Projects</h2>
    
    <div class="projects-container">
      <div 
        v-for="(project, index) in projects" 
        :key="index" 
        class="project-card"
        :class="{ 
          'right-image': index % 2 !== 0,
          'left-image': index % 2 === 0,
          'animate': projectVisibility[index]
        }"
      >
        <!-- 偶数项目：图片在左 -->
        <template v-if="index % 2 === 0">
          <div class="project-image-container">
            <img :src="project.image" :alt="project.title" class="project-image main-image" />
            <img
              v-for="(overlay, i) in project.overlayImages"
              :key="i"
              :src="overlay"
              alt="Overlay View"
              class="project-image overlay-image"
              :class="[`overlay-${i + 1}`]"
            />
          </div>
          
          <div class="project-details">
            <div class="project-header">
              <h3 class="project-title">{{ project.title }}</h3>
              <div class="project-links">
                <a
                  v-if="project.demoUrl && project.demoUrl !== '#'"
                  :href="project.demoUrl"
                  target="_blank"
                  rel="noopener"
                  class="icon-link"
                  aria-label="Live"
                >
                  <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M14 3v2h3.59l-9.83 9.83 1.41 1.41L19 6.41V10h2V3h-7zM5 5h5V3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2v-5h-2v5H5V5z"/>
                  </svg>
                </a>
                <a :href="project.githubUrl" target="_blank" class="icon-link" aria-label="GitHub">
                  <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/>
                  </svg>
                </a>
              </div>
            </div>
            
            <p class="project-description">{{ project.description }}</p>
            
            <div class="project-tags">
              <span v-for="tag in project.tags" :key="tag" class="project-tag">
                {{ tag }}
              </span>
            </div>
          </div>
        </template>
        
        <!-- 奇数项目：图片在右 -->
        <template v-else>
          <div class="project-details">
            <div class="project-header">
              <h3 class="project-title">{{ project.title }}</h3>
              <div class="project-links">
                <a
                  v-if="project.demoUrl && project.demoUrl !== '#'"
                  :href="project.demoUrl"
                  target="_blank"
                  rel="noopener"
                  class="icon-link"
                  aria-label="Live"
                >
                  <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M14 3v2h3.59l-9.83 9.83 1.41 1.41L19 6.41V10h2V3h-7zM5 5h5V3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2v-5h-2v5H5V5z"/>
                  </svg>
                </a>
                <a :href="project.githubUrl" target="_blank" class="icon-link" aria-label="GitHub">
                  <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/>
                  </svg>
                </a>
              </div>
            </div>
            
            <p class="project-description">{{ project.description }}</p>
            
            <div class="project-tags">
              <span v-for="tag in project.tags" :key="tag" class="project-tag">
                {{ tag }}
              </span>
            </div>
          </div>
          
          <div class="project-image-container">
            <img :src="project.image" :alt="project.title" class="project-image main-image" />
            <img
              v-for="(overlay, i) in project.overlayImages"
              :key="i"
              :src="overlay"
              alt="Overlay View"
              class="project-image overlay-image"
              :class="[`overlay-${i + 1}`]"
            />
          </div>
        </template>
      </div>
    </div>
  </div>
</template>

<style scoped>
.projects-section {
  min-height: 100vh;
  padding: 4rem 1.5rem;
  display: flex;
  flex-direction: column;
  max-width: 1200px;
  margin: 0 auto;
}

.section-title {
  font-size: 3.5rem;
  font-weight: 800;
  margin-bottom: 4rem;
  text-align: center;
}

.projects-container {
  display: flex;
  flex-direction: column;
  gap: 8rem;
  margin-top: 2rem;
}

.project-card {
  display: flex;
  gap: 4rem;
  position: relative;
  opacity: 0;
  transform: translateY(50px);
  transition: opacity 0.8s ease, transform 0.8s ease;
}

.project-card.animate {
  opacity: 1;
  transform: translateY(0);
}

.project-card.left-image {
  flex-direction: row;
}

.project-card.right-image {
  flex-direction: row-reverse;
}

.project-image-container {
  flex: 1;
  background-color: transparent;
  border-radius: 12px;
  overflow: visible;
  min-height: 420px;
  position: relative;
  margin: 20px 20px 20px 40px;
  perspective: 1100px;
  isolation: isolate;
}

.project-image-container::before {
  content: '';
  position: absolute;
  top: -10px;
  left: -10px;
  width: 100%;
  height: 100%;
  border: 2px solid #333;
  border-radius: 12px;
  z-index: -1;
}

/* 柔和氛围光 */
.project-image-container::after {
  content: '';
  position: absolute;
  inset: -40px;
  background:
    radial-gradient(380px 220px at 10% 0%, rgba(88, 166, 255, 0.14), transparent 60%),
    radial-gradient(320px 200px at 90% 100%, rgba(251, 109, 160, 0.12), transparent 60%);
  filter: blur(22px);
  z-index: -2;
}

.project-image.main-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 16px;
  box-shadow: 0 25px 50px rgba(0, 0, 0, 0.22);
  transform: translate(18px, 12px) rotateX(1.2deg) rotateY(-1.2deg);
  transition: transform 0.6s ease, box-shadow 0.6s ease;
  outline: 1px solid rgba(0,0,0,0.06);
}

.project-image.overlay-image {
  position: absolute;
  width: auto;
  height: 68%;
  object-fit: cover;
  border-radius: 14px;
  border: 8px solid rgba(255,255,255,0.95);
  background-color: #fff;
  z-index: 3;
  filter: drop-shadow(0 14px 28px rgba(0,0,0,0.18));
  transform: translateZ(0);
  transition: transform 0.6s ease, filter 0.6s ease, box-shadow 0.6s ease;
}

/* 多覆盖图布局：避免重叠并形成精致分层 */
.project-image.overlay-image.overlay-1 {
  top: -26px;
  left: -26px;
  right: auto;
  bottom: auto;
  height: 64%;
  transform: rotate(-6deg);
}

.project-image.overlay-image.overlay-2 {
  bottom: -28px;
  right: -6px;
  left: auto;
  top: auto;
  height: 56%;
  transform: rotate(7deg);
}

.project-image-container:hover .project-image.main-image {
  transform: translate(8px, 4px) scale(1.02) rotateX(0) rotateY(0);
  box-shadow: 0 35px 70px rgba(0, 0, 0, 0.28);
}

.project-image-container:hover .project-image.overlay-image.overlay-1 {
  transform: translate(-6px, -4px) rotate(-3deg) scale(1.03);
}

.project-image-container:hover .project-image.overlay-image.overlay-2 {
  transform: translate(6px, 4px) rotate(5deg) scale(1.05);
}

.project-details {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 1rem;
}

.project-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1.5rem;
}

.project-title {
  font-size: 2.2rem;
  font-weight: 800;
  margin: 0;
  line-height: 1.2;
}

.project-links {
  display: flex;
  gap: 1rem;
}

.icon-link {
  color: #333;
  transition: color 0.2s, transform 0.2s;
}

.icon-link:hover {
  color: #0077ff;
  transform: translateY(-3px);
}

/* 文字按钮已移除，保留图标风格 */

.project-description {
  font-size: 1.15rem;
  line-height: 1.7;
  margin-bottom: 2.5rem;
  color: #333;
}

.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.8rem;
}

.project-tag {
  background-color: #2d2d2d;
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  font-size: 0.8rem;
  font-weight: 600;
  text-transform: uppercase;
  transition: transform 0.2s, background-color 0.2s;
}

.project-tag:hover {
  transform: translateY(-2px);
  background-color: #000;
}

.dark .project-image-container {
  background-color: #2d2d3a;
}

.dark .icon-link {
  color: #eee;
}

.dark .icon-link:hover {
  color: #58a6ff;
}

.dark .project-description {
  color: #eee;
}

.dark .project-tag {
  background-color: #444;
}

.dark .project-tag:hover {
  background-color: #555;
}

.dark .project-image-container::before {
  border-color: #555;
}

.dark .project-image.main-image {
  box-shadow: 15px 15px 30px rgba(0, 0, 0, 0.4);
}

.dark .project-image.overlay-image {
  box-shadow: 10px 10px 20px rgba(0, 0, 0, 0.5);
}

.dark .project-image-container:hover .project-image.main-image {
  box-shadow: 20px 20px 40px rgba(0, 0, 0, 0.6);
}

.dark .project-image-container:hover .project-image.overlay-image {
  box-shadow: 15px 15px 30px rgba(0, 0, 0, 0.7);
}

.project-card.right-image .project-image-container {
  margin: 20px 40px 20px 20px;
}

@media (max-width: 850px) {
  .project-card.left-image, 
  .project-card.right-image {
    flex-direction: column;
    gap: 2rem;
  }
  
  .section-title {
    font-size: 2.5rem;
    margin-bottom: 2.5rem;
  }
  
  .project-title {
    font-size: 1.8rem;
  }
  
  .project-description {
    font-size: 1rem;
    margin-bottom: 2rem;
  }
  
  .projects-container {
    gap: 5rem;
  }
  
  .project-image-container {
    min-height: 300px;
    margin: 10px 0 0 0;
  }

  .project-image.main-image {
    transform: translate(8px, 6px);
  }

  .project-image.overlay-image {
    height: 54%;
    border-width: 6px;
  }

  .project-image.overlay-image.overlay-1 {
    top: -14px;
    left: -10px;
  }

  .project-image.overlay-image.overlay-2 {
    bottom: -14px;
    right: -4px;
    height: 50%;
  }
}
</style> 