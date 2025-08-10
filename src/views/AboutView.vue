<script setup lang="ts">
// About view component
</script>

<template>
  <div class="about-section">
    <h2 class="section-title">About Me</h2>
    
    <div class="about-content slide-up">
      <p class="about-text">
        After completing my undergraduate degree in <em>Mechanical Engineering at Donghua University</em>, I found a deep passion for programming. This journey began with classes in computer science fundamentals, which led me directly to <em>Java backend development</em>. After several hands-on projects, I confirmed my commitment to this career path. Currently, I am pursuing a Master's degree in <em>Electronic Information</em> at <em>Donghua University</em>. I thrive on the challenges of coding and the satisfaction that comes from solving complex problems. I am proficient in technologies such as <em>Spring Boot, MyBatis, MySQL, Redis, and RabbitMQ</em>, and have a solid understanding of <em>Java development</em>.
      </p>
      
      <p class="about-text">
        In my spare time, I enjoy learning new skills and building fun projects. I am eager to learn, embrace challenges, and look forward to contributing my skills to future projects.
        </p>
    </div>
  </div>
</template>

<style scoped>
.about-section {
  min-height: 100vh;
  padding: 4rem 1.5rem;
  max-width: 950px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.section-title {
  font-size: 3.5rem;
  font-weight: 800;
  margin-bottom: 3rem;
  text-align: center;
}

.about-content {
  margin: 0 auto;
  text-align: center;
  max-width: 800px;
}

.about-text {
  font-size: 1.2rem;
  line-height: 1.8;
  color: #222;
  margin-bottom: 2rem;
  letter-spacing: 0.3px;
  text-align: center;
}

.about-text em {
  font-style: italic;
  font-weight: 500;
}

.dark .about-text {
  color: #eee;
}

@media (max-width: 768px) {
  .about-section {
    padding: 2rem 1rem;
}

  .section-title {
    font-size: 2.8rem;
    margin-bottom: 2rem;
  }
  
  .about-text {
    font-size: 1.1rem;
  line-height: 1.6;
  }
}
</style> 