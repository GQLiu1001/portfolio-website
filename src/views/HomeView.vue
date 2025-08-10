<script setup lang="ts">
// Home view component
import profileImage from '../assets/image/pic.jpg'
import { ref, onMounted } from 'vue'

const typewriterText = ref('')
const fullText = "I focus on Java and enjoy building projects."
const typeSpeed = 50
const eraseSpeed = 30
const pauseDelay = 2000
let charIndex = 0
let isTyping = true
let isPaused = false

// 添加复制成功提示状态
const showCopyMsg = ref(false)

function typeWriter() {
  if (isTyping) {
    // 打字阶段
    if (charIndex < fullText.length) {
      typewriterText.value += fullText.charAt(charIndex)
      charIndex++
      setTimeout(typeWriter, typeSpeed)
    } else {
      // 打字完成，暂停一段时间
      isPaused = true
      setTimeout(() => {
        isPaused = false
        isTyping = false
        typeWriter()
      }, pauseDelay)
    }
  } else {
    // 删除阶段
    if (typewriterText.value.length > 0) {
      typewriterText.value = typewriterText.value.substring(0, typewriterText.value.length - 1)
      setTimeout(typeWriter, eraseSpeed)
    } else {
      // 删除完成，重新开始打字
      charIndex = 0
      isTyping = true
      setTimeout(typeWriter, typeSpeed)
    }
  }
}

// 添加复制邮箱到剪贴板的函数
function copyEmail(event: MouseEvent) {
  event.preventDefault()
  const email = '1196551872@qq.com'
  navigator.clipboard.writeText(email).then(() => {
    showCopyMsg.value = true
    setTimeout(() => {
      showCopyMsg.value = false
    }, 2000)
  })
}

onMounted(() => {
  setTimeout(() => {
    typeWriter()
  }, 500)
})
</script>

<template>
  <div class="home-container">
    <div class="hero">
      <div class="avatar-container">
        <div class="avatar">
          <img :src="profileImage" alt="Profile Photo" class="avatar-img" />
          <span class="hand">👋</span>
        </div>
      </div>
      
      <div class="intro fade-in">
        <div class="greeting">Hello, I'm Liu Guoqing a</div>
        <h1 class="name">Backend Developer</h1>
        <div class="subtitle">
          <p class="typewriter-text">{{ typewriterText }}<span class="typewriter-cursor">|</span></p>
        </div>
        
        <div class="cta-buttons">
          <a href="#" @click="copyEmail" class="contact-button">
            Contact Me <span class="contact-icon">✉️</span>
            <span v-if="showCopyMsg" class="copy-msg">Email copied!</span>
          </a>
          <div class="social-links">
            <a href="https://space.bilibili.com/13237349?spm_id_from=333.1007.0.0" target="_blank" class="social-link">
              <svg class="bilibili-icon" viewBox="0 0 24 24" width="18" height="18" fill="currentColor">
                <path d="M17.813 4.653h.854c1.51.054 2.769.578 3.773 1.574 1.004.995 1.524 2.249 1.56 3.76v7.36c-.036 1.51-.556 2.769-1.56 3.773s-2.262 1.524-3.773 1.56H5.333c-1.51-.036-2.769-.556-3.773-1.56S.036 18.858 0 17.347v-7.36c.036-1.511.556-2.765 1.56-3.76 1.004-.996 2.262-1.52 3.773-1.574h.774l-1.174-1.12a1.234 1.234 0 0 1-.373-.906c0-.356.124-.658.373-.907l.027-.027c.267-.249.573-.373.92-.373.347 0 .653.124.92.373L9.653 4.44c.071.071.134.142.187.213h4.267a.836.836 0 0 1 .16-.213l2.853-2.747c.267-.249.573-.373.92-.373.347 0 .662.151.929.4.267.249.391.551.391.907 0 .355-.124.657-.373.906L17.813 4.653zM5.333 7.24c-.746.018-1.373.276-1.88.773-.506.498-.769 1.13-.786 1.894v7.52c.017.764.28 1.395.786 1.893.507.498 1.134.756 1.88.773h13.334c.746-.017 1.373-.275 1.88-.773.506-.498.769-1.129.786-1.893v-7.52c-.017-.765-.28-1.396-.786-1.894-.507-.497-1.134-.755-1.88-.773H5.333zM8 11.107c.373 0 .684.124.933.373.25.249.383.569.4.96v1.173c-.017.391-.15.711-.4.96-.249.25-.56.374-.933.374s-.684-.125-.933-.374c-.25-.249-.383-.569-.4-.96V12.44c.017-.391.15-.711.4-.96.249-.249.56-.373.933-.373zm8 0c.373 0 .684.124.933.373.25.249.383.569.4.96v1.173c-.017.391-.15.711-.4.96-.249.25-.56.374-.933.374s-.684-.125-.933-.374c-.25-.249-.383-.569-.4-.96V12.44c.017-.391.15-.711.4-.96.249-.249.56-.373.933-.373z"/>
              </svg>
            </a>
            <a href="https://github.com/GQLiu1001" target="_blank" class="social-link">
              <svg class="github-icon" viewBox="0 0 24 24" width="18" height="18" fill="currentColor">
                <path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/>
              </svg>
            </a>
          </div>
        </div>
      </div>
    </div>

    <div class="scroll-indicator">
      <div class="scroll-arrow"></div>
    </div>
  </div>
</template>

<style scoped>
.home-container {
  min-height: calc(100vh - 80px);
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.hero {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  flex: 1;
  padding: 0 1rem;
}

.avatar-container {
  margin-bottom: 2rem;
}

.avatar {
  width: 180px;
  height: 180px;
  position: relative;
}

.avatar-img {
  width: 100%;
  height: 100%;
  border-radius: 50%;
  object-fit: cover;
  border: 4px solid white;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
  filter: grayscale(0.9) contrast(1.2);
  transition: filter 0.3s ease, transform 0.3s ease;
}

.avatar-img:hover {
  filter: grayscale(0.4) contrast(1.1);
  transform: scale(1.05);
}

.dark .avatar-img {
  border-color: #222;
}

.hand {
  position: absolute;
  bottom: 0;
  right: -30px;
  font-size: 2.2rem;
  filter: drop-shadow(0 2px 5px rgba(0,0,0,0.1));
  animation: wave 2.5s infinite;
  transform-origin: 70% 70%;
}

@keyframes wave {
  0% { transform: rotate(0deg); }
  10% { transform: rotate(16deg); }
  20% { transform: rotate(0deg); }
  30% { transform: rotate(16deg); }
  40% { transform: rotate(0deg); }
  100% { transform: rotate(0deg); }
}

.intro {
  max-width: 95vw;
  width: 95vw;
  margin: 0 auto;
}

.greeting {
  font-size: 2rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.name {
  font-size: 4.5rem;
  font-weight: 900;
  margin: 0.5rem 0;
  letter-spacing: -2px;
  line-height: 1.1;
}

.subtitle {
  font-size: 1.5rem;
  margin: 1.5rem 0 2.5rem;
  line-height: 1.5;
  min-height: 4.5rem;
  white-space: nowrap;
  overflow: hidden;
  max-width: 100%;
  width: 100%;
  height: 4.5rem;
}

.typewriter-text {
  display: inline-block;
  font-weight: 800;
  max-width: 100%;
}

.typewriter-cursor {
  display: inline-block;
  width: 2px;
  animation: blink 0.7s infinite;
  font-weight: 800;
}

@keyframes blink {
  0% { opacity: 1; }
  50% { opacity: 0; }
  100% { opacity: 1; }
}

.cta-buttons {
  display: flex;
  justify-content: center;
  gap: 2rem;
  margin-top: 1rem;
}

.contact-button {
  background-color: black;
  color: white;
  padding: 0.8rem 1.5rem;
  border-radius: 50px;
  font-weight: 600;
  text-decoration: none;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s, box-shadow 0.2s;
  position: relative;
}

.dark .contact-button {
  background-color: white;
  color: black;
}

.contact-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.15);
}

.contact-icon {
  font-size: 1.2rem;
}

.copy-msg {
  position: absolute;
  bottom: -30px;
  left: 50%;
  transform: translateX(-50%);
  background: rgba(0, 0, 0, 0.8);
  color: white;
  padding: 4px 10px;
  border-radius: 4px;
  font-size: 12px;
  white-space: nowrap;
  animation: fadeIn 0.3s;
  z-index: 10;
}

.dark .copy-msg {
  background: rgba(255, 255, 255, 0.8);
  color: black;
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

.social-links {
  display: flex;
  gap: 1rem;
  align-items: center;
}

.social-link {
  width: 42px;
  height: 42px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: black;
  color: white;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  text-decoration: none;
  transition: transform 0.2s;
}

.dark .social-link {
  background-color: white;
  color: black;
}

.social-link:hover {
  transform: scale(1.1);
}

.github-icon, .bilibili-icon {
  width: 18px;
  height: 18px;
}

.scroll-indicator {
  display: flex;
  justify-content: center;
  margin-bottom: 2rem;
}

.scroll-arrow {
  width: 30px;
  height: 30px;
  border: solid rgba(0, 0, 0, 0.3);
  border-width: 0 2px 2px 0;
  transform: rotate(45deg);
  animation: pulse 2s infinite;
}

.dark .scroll-arrow {
  border-color: rgba(255, 255, 255, 0.3);
}

@keyframes pulse {
  0% { opacity: 0.4; }
  50% { opacity: 0.8; }
  100% { opacity: 0.4; }
}

@media (max-width: 768px) {
  .name {
    font-size: 3rem;
  }
  
  .greeting {
    font-size: 1.5rem;
  }
  
  .subtitle {
    font-size: 1.2rem;
    min-height: 3.5rem;
    height: 3.5rem;
    margin: 1rem 0 2rem;
    white-space: normal;
    overflow: hidden;
  }
  
  .typewriter-text {
    display: inline-block;
    max-width: 100%;
    white-space: normal;
    word-wrap: break-word;
  }
  
  .cta-buttons {
    flex-direction: column;
    align-items: center;
    gap: 1rem;
  }
}
</style>
