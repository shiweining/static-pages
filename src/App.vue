<template>
  <div class="app-wrapper">
    <!-- 背景装饰 -->
    <div class="bg-decoration">
      <div class="bg-blob blob-1"></div>
      <div class="bg-blob blob-2"></div>
      <div class="bg-blob blob-3"></div>
    </div>

    <!-- 顶部导航链接 -->
    <nav class="top-nav">
      <div class="nav-links">
        <a href="https://github.com" target="_blank" rel="noopener" title="GitHub">
          <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
            <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
          </svg>
        </a>
        <a href="https://vitejs.dev" target="_blank" rel="noopener" title="Vite">
          <svg width="20" height="20" viewBox="0 0 410 404" fill="none">
            <path d="M399.641 59.5246L215.643 388.545C211.844 395.338 202.084 395.378 198.228 388.618L10.5817 59.5563C6.38087 52.1896 12.6802 43.2665 21.0281 44.7586L205.223 77.6824C206.398 77.8924 207.601 77.8904 208.776 77.6763L389.119 44.8058C397.439 43.2894 403.768 52.1434 399.641 59.5246Z" fill="url(#paint0_linear)"/>
            <path d="M292.965 1.5744L156.801 28.2552C154.563 28.6937 152.906 30.5903 152.771 32.8664L144.395 174.33C144.198 177.662 147.258 180.248 150.51 179.498L188.42 170.749C191.967 169.931 195.172 173.055 194.443 176.622L183.18 231.775C182.422 235.487 185.907 238.661 189.532 237.56L212.947 230.446C216.577 229.344 220.065 232.527 219.297 236.242L201.398 322.875C200.278 328.294 207.486 331.249 210.492 326.603L212.5 323.5L323.454 102.072C325.312 98.3645 322.108 94.137 318.036 94.9228L279.014 102.454C275.347 103.161 272.227 99.746 273.262 96.1583L298.731 7.86689C299.767 4.27314 296.636 0.855181 292.965 1.5744Z" fill="url(#paint1_linear)"/>
            <defs>
              <linearGradient id="paint0_linear" x1="6.00017" y1="32.9999" x2="235" y2="344" gradientUnits="userSpaceOnUse">
                <stop stop-color="#41D1FF"/>
                <stop offset="1" stop-color="#BD34FE"/>
              </linearGradient>
              <linearGradient id="paint1_linear" x1="194.651" y1="8.81818" x2="236.076" y2="292.989" gradientUnits="userSpaceOnUse">
                <stop stop-color="#FFEA83"/>
                <stop offset="0.0833333" stop-color="#FFDD35"/>
                <stop offset="1" stop-color="#FFA800"/>
              </linearGradient>
            </defs>
          </svg>
        </a>
        <a href="https://vuejs.org" target="_blank" rel="noopener" title="Vue">
          <svg width="20" height="20" viewBox="0 0 261.76 226.69">
            <path d="M161.096.001l-30.224 52.35L100.647.002H-.005L130.872 226.69 261.749 0z" fill="#41b883"/>
            <path d="M161.096.001l-30.224 52.35L100.647.002H52.346l78.526 136.01L209.398.001z" fill="#34495e"/>
          </svg>
        </a>
      </div>
    </nav>

    <div class="container">
      <!-- 英雄区域 -->
      <header class="hero">
        <h1 class="hero-title">
          <span class="title-line gradient-text">静态资源中心</span>
        </h1>
        <p class="hero-subtitle">
          统一托管多个项目的静态资源，简洁高效的展示方案
        </p>
        <div class="hero-meta">
          <div class="meta-item">
            <span class="meta-icon">🚀</span>
            <span>快速部署</span>
          </div>
          <div class="meta-item">
            <span class="meta-icon">📦</span>
            <span>集中管理</span>
          </div>
          <div class="meta-item">
            <span class="meta-icon">⚡</span>
            <span>高效访问</span>
          </div>
        </div>
      </header>

      <!-- 项目列表 -->
      <main class="projects-section">
        <div class="section-header">
          <h2 class="section-title">项目列表</h2>
        </div>

        <!-- 加载状态 -->
        <div v-if="loading" class="loading-state">
          <div class="spinner"></div>
          <p>加载中...</p>
        </div>

        <!-- 错误状态 -->
        <div v-else-if="error" class="error-state">
          <div class="error-icon">⚠️</div>
          <p>{{ error }}</p>
        </div>

        <!-- 项目列表 -->
        <div v-else-if="projects.length > 0" class="projects-grid">
          <div
            v-for="project in projects"
            :key="project.id"
            class="project-card"
          >
            <div class="card-header">
              <div class="card-icon">{{ project.icon }}</div>
              <div class="card-status">在线</div>
            </div>
            <h3 class="card-title">{{ project.name }}</h3>
            <p class="card-description">{{ project.description }}</p>
            <a
              :href="project.url"
              class="card-button"
              target="_blank"
              rel="noopener noreferrer"
            >
              <span>访问项目</span>
              <svg width="16" height="16" viewBox="0 0 16 16" fill="none">
                <path d="M6 3L11 8L6 13" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
              </svg>
            </a>
          </div>
        </div>

        <!-- 空状态 -->
        <div v-else class="empty-state">
          <div class="empty-icon">📦</div>
          <p>暂无项目</p>
        </div>
      </main>
    </div>

    <footer class="footer">
      <p>© 2026 - 使用 Vue 3 + Vite 构建</p>
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const projects = ref([])
const loading = ref(true)
const error = ref(null)

// 动态加载项目列表
onMounted(async () => {
  try {
    const response = await fetch('./projects.json')
    if (!response.ok) {
      throw new Error('Failed to load projects')
    }
    const data = await response.json()
    projects.value = data.projects
  } catch (err) {
    console.error('Error loading projects:', err)
    error.value = '加载项目列表失败'
  } finally {
    loading.value = false
  }
})
</script>

<style scoped>
/* 整体布局 */
.app-wrapper {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  position: relative;
  overflow-x: hidden;
}

/* 顶部导航 */
.top-nav {
  position: fixed;
  top: 1.5rem;
  right: 2rem;
  z-index: 100;
}

.nav-links {
  display: flex;
  gap: 1rem;
  align-items: center;
}

.nav-links a {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  background: rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.15);
  border-radius: 50%;
  color: rgba(255, 255, 255, 0.8);
  transition: all 0.3s ease;
}

.nav-links a:hover {
  background: rgba(102, 126, 234, 0.2);
  border-color: rgba(102, 126, 234, 0.5);
  color: #667eea;
  transform: translateY(-2px);
}

.nav-links svg {
  transition: transform 0.3s ease;
}

.nav-links a:hover svg {
  transform: scale(1.1);
}

/* 背景装饰 */
.bg-decoration {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: -1;
  pointer-events: none;
}

.bg-blob {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  opacity: 0.3;
  animation: float 20s infinite ease-in-out;
}

.blob-1 {
  width: 500px;
  height: 500px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  top: -200px;
  right: -100px;
  animation-delay: 0s;
}

.blob-2 {
  width: 400px;
  height: 400px;
  background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
  bottom: -150px;
  left: -100px;
  animation-delay: -10s;
}

.blob-3 {
  width: 300px;
  height: 300px;
  background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  animation-delay: -5s;
}

@keyframes float {
  0%, 100% {
    transform: translate(0, 0) scale(1);
  }
  33% {
    transform: translate(30px, -50px) scale(1.1);
  }
  66% {
    transform: translate(-20px, 30px) scale(0.9);
  }
}

/* 容器 */
.container {
  flex: 1;
  max-width: 1200px;
  margin: 0 auto;
  padding: 1rem 2rem;
  width: 100%;
  position: relative;
  z-index: 1;
}

/* 英雄区域 */
.hero {
  text-align: center;
  padding: 1.5rem 0 1rem;
  margin-bottom: 2rem;
}

.hero-title {
  font-size: 3rem;
  font-weight: 800;
  line-height: 1.2;
  margin: 0 0 1rem 0;
  letter-spacing: -0.02em;
}

.title-line {
  display: block;
}

.gradient-text {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 50%, #f093fb 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  animation: gradient-shift 3s ease infinite;
  background-size: 200% 200%;
}

@keyframes gradient-shift {
  0%, 100% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
}

.hero-subtitle {
  font-size: 1.05rem;
  opacity: 0.8;
  max-width: 600px;
  margin: 0 auto 1.25rem;
  line-height: 1.6;
}

.hero-meta {
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.meta-item {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.6rem 1.25rem;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 12px;
  font-size: 0.875rem;
  font-weight: 500;
  backdrop-filter: blur(10px);
  transition: all 0.3s ease;
}

.meta-item:hover {
  background: rgba(255, 255, 255, 0.08);
  transform: translateY(-2px);
}

.meta-icon {
  font-size: 1.1rem;
}

/* 项目区域 */
.projects-section {
  margin-bottom: 2.5rem;
}

.section-header {
  text-align: center;
  margin-bottom: 1.75rem;
}

.section-title {
  font-size: 1.65rem;
  font-weight: 700;
  margin-bottom: 0;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 1.5rem;
}

/* 项目卡片 */
.project-card {
  position: relative;
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  padding: 1.75rem;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  overflow: hidden;
}

.project-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, rgba(102, 126, 234, 0.1) 0%, rgba(118, 75, 162, 0.1) 100%);
  opacity: 0;
  transition: opacity 0.4s ease;
}

.project-card:hover {
  transform: translateY(-10px) scale(1.02);
  box-shadow: 0 20px 40px rgba(102, 126, 234, 0.3);
  border-color: rgba(102, 126, 234, 0.5);
}

.project-card:hover::before {
  opacity: 1;
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 1rem;
  position: relative;
  z-index: 1;
}

.card-icon {
  font-size: 3rem;
  line-height: 1;
  filter: drop-shadow(0 4px 8px rgba(0, 0, 0, 0.2));
}

.card-status {
  display: inline-block;
  padding: 0.25rem 0.75rem;
  background: rgba(34, 197, 94, 0.15);
  border: 1px solid rgba(34, 197, 94, 0.3);
  color: #22c55e;
  border-radius: 20px;
  font-size: 0.75rem;
  font-weight: 600;
  letter-spacing: 0.02em;
}

.card-title {
  font-size: 1.5rem;
  font-weight: 700;
  margin-bottom: 0.75rem;
  position: relative;
  z-index: 1;
}

.card-description {
  color: rgba(255, 255, 255, 0.7);
  margin-bottom: 1.5rem;
  line-height: 1.6;
  font-size: 0.95rem;
  position: relative;
  z-index: 1;
}

.card-button {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1.5rem;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  text-decoration: none;
  border-radius: 12px;
  font-weight: 600;
  font-size: 0.95rem;
  transition: all 0.3s ease;
  position: relative;
  z-index: 1;
  overflow: hidden;
}

.card-button::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.3), transparent);
  transition: left 0.5s ease;
}

.card-button:hover::before {
  left: 100%;
}

.card-button:hover {
  transform: translateX(4px);
  box-shadow: 0 4px 16px rgba(102, 126, 234, 0.5);
}

.card-button svg {
  transition: transform 0.3s ease;
}

.card-button:hover svg {
  transform: translateX(4px);
}

/* 加载、错误和空状态 */
.loading-state,
.error-state,
.empty-state {
  text-align: center;
  padding: 4rem 2rem;
}

.loading-state {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
}

.spinner {
  width: 48px;
  height: 48px;
  border: 4px solid rgba(102, 126, 234, 0.1);
  border-top-color: #667eea;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}

.loading-state p,
.error-state p,
.empty-state p {
  font-size: 1rem;
  opacity: 0.7;
  margin-top: 0.5rem;
}

.error-icon,
.empty-icon {
  font-size: 4rem;
  margin-bottom: 1rem;
  opacity: 0.6;
}

.error-state {
  color: #ef4444;
}

.empty-state {
  opacity: 0.6;
}

/* 页脚 */
.footer {
  padding: 1.5rem 0;
  text-align: center;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  margin-top: auto;
  position: relative;
  z-index: 1;
  font-size: 0.9rem;
  opacity: 0.6;
}

/* 亮色模式适配 */
@media (prefers-color-scheme: light) {
  .bg-blob {
    opacity: 0.15;
  }

  .nav-links a {
    background: rgba(0, 0, 0, 0.05);
    border-color: rgba(0, 0, 0, 0.1);
    color: rgba(0, 0, 0, 0.7);
  }

  .nav-links a:hover {
    background: rgba(102, 126, 234, 0.15);
    color: #667eea;
  }

  .meta-item {
    background: rgba(0, 0, 0, 0.03);
    border-color: rgba(0, 0, 0, 0.1);
  }

  .meta-item:hover {
    background: rgba(0, 0, 0, 0.05);
  }

  .project-card {
    background: rgba(255, 255, 255, 0.8);
    border-color: rgba(0, 0, 0, 0.1);
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
  }

  .project-card::before {
    background: linear-gradient(135deg, rgba(102, 126, 234, 0.08) 0%, rgba(118, 75, 162, 0.08) 100%);
  }

  .project-card:hover {
    box-shadow: 0 20px 40px rgba(102, 126, 234, 0.2);
  }

  .card-description {
    color: rgba(0, 0, 0, 0.65);
  }

  .footer {
    border-top-color: rgba(0, 0, 0, 0.1);
  }
}

/* 响应式设计 */
@media (max-width: 768px) {
  .top-nav {
    top: 1rem;
    right: 1rem;
  }

  .nav-links {
    gap: 0.75rem;
  }

  .nav-links a {
    width: 36px;
    height: 36px;
  }

  .nav-links svg {
    width: 18px;
    height: 18px;
  }

  .hero {
    padding: 1.25rem 0 0.75rem;
    margin-bottom: 1.5rem;
  }

  .hero-title {
    font-size: 2rem;
  }

  .hero-subtitle {
    font-size: 0.95rem;
  }

  .hero-meta {
    gap: 1rem;
  }

  .meta-item {
    padding: 0.5rem 1rem;
    font-size: 0.85rem;
  }

  .section-title {
    font-size: 1.5rem;
  }

  .section-header {
    margin-bottom: 1.5rem;
  }

  .projects-grid {
    grid-template-columns: 1fr;
  }

  .blob-1,
  .blob-2,
  .blob-3 {
    width: 300px;
    height: 300px;
  }
}

@media (max-width: 480px) {
  .container {
    padding: 1rem;
  }

  .top-nav {
    top: 0.75rem;
    right: 0.75rem;
  }

  .nav-links a {
    width: 32px;
    height: 32px;
  }

  .nav-links svg {
    width: 16px;
    height: 16px;
  }

  .hero {
    padding: 1rem 0 0.5rem;
  }

  .hero-title {
    font-size: 1.75rem;
  }

  .footer {
    font-size: 0.8rem;
  }
}
</style>
