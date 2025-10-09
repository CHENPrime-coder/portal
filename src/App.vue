<script setup>
import { onMounted, onUnmounted, ref } from 'vue'

const services = ref([
  {
    id: 1,
    title: '个人博客',
    description: '技术分享与生活记录',
    icon: '📝',
    shortcut: '/blog',
    link: 'https://www.chenprime.xyz',
    color: 'from-blue-500 to-blue-600'
  },
  {
    id: 2,
    title: '视频站',
    description: 'Luna TV',
    icon: '📺',
    shortcut: '/tv',
    link: 'https://vxmspqeuohoi.ap-northeast-1.clawcloudrun.com',
    color: 'from-gray-500 to-gray-600'
  },
  {
    id: 3,
    title: '网盘站',
    description: 'OpenList',
    icon: '💾',
    shortcut: '/disk',
    link: 'https://hbudjbzq.us-west-1.clawcloudrun.com',
    color: 'from-gray-500 to-gray-600'
  },
  {
    id: 4,
    title: '代码仓库',
    description: 'GitHub 项目管理',
    icon: '💻',
    shortcut: '/github',
    link: 'https://github.com/chenprime-coder',
    color: 'from-gray-500 to-gray-600'
  }
])

const socialLinks = ref([
  { name: 'Email', icon: '✉️', link: 'mailto:chenbprime@gmail.com' },
  { name: 'Steam', icon: '🎮', link: 'https://steamcommunity.com/id/chenprime' }
])

// javascript, c#, kotlin, java, python
const skills = ref([  
  {
    name: 'C#',
    color: 'from-blue-400 to-blue-500',
    bgColor: 'bg-blue-500/20',
    textColor: 'text-blue-300'
  },
  {
    name: 'Kotlin',
    color: 'from-purple-400 to-purple-500',
    bgColor: 'bg-purple-500/20',
    textColor: 'text-purple-300'
  },
  {
    name: 'JavaScript',
    color: 'from-green-400 to-green-500',
    bgColor: 'bg-green-500/20',
    textColor: 'text-green-300'
  },
  {
    name: 'Java',
    color: 'from-orange-400 to-orange-500',
    bgColor: 'bg-orange-500/20',
    textColor: 'text-orange-300'
  },
  {
    name: 'Python',
    color: 'from-yellow-400 to-yellow-500',
    bgColor: 'bg-yellow-500/20',
    textColor: 'text-yellow-300'
  }
])

const openNewTab = (url) => {
  window.open(url, '_blank')
}

// 检查并处理 URL 路径跳转
const handleUrlRedirect = () => {
  const path = window.location.pathname
  const service = services.value.find(service => service.shortcut === path)

  // 如果路径不为空且在服务映射中存在
  if (service) {
    window.location.href = service.link
  }
}

const handlePopState = () => {
  handleUrlRedirect()
}

onMounted(() => {
  // 页面加载时检查 URL
  handleUrlRedirect()
  
  // 监听浏览器前进后退按钮
  window.addEventListener('popstate', handlePopState)
})

onUnmounted(() => {
  window.removeEventListener('popstate', handlePopState)
})
</script>

<template>
  <div class="min-h-screen bg-gradient-to-br from-slate-900 via-purple-900 to-slate-900 text-white overflow-hidden">
    <!-- 顶部个人信息区域 (25% 高度) -->
    <header class="h-1/4 flex items-center justify-center px-6 md:px-12 py-4 md:py-6">
      <div class="flex flex-col md:flex-row items-center md:space-x-12 space-y-6 md:space-y-0 w-full max-w-4xl">
        <!-- 头像 -->
        <div class="relative flex-shrink-0">
          <div class="w-20 h-20 md:w-28 md:h-28 rounded-full bg-gradient-to-r from-blue-400 to-purple-500 p-1">
            <img class="w-full h-full rounded-full bg-slate-800 flex items-center justify-center text-2xl md:text-4xl" src="/profile.webp" alt="Profile Picture"/>
          </div>
          <div class="absolute -bottom-1 -right-1 w-6 h-6 md:w-8 md:h-8 bg-green-500 rounded-full border-3 md:border-4 border-slate-900"></div>
        </div>
        
        <!-- 个人信息 -->
        <div class="text-center md:text-left flex-1">
          <h1 class="text-3xl md:text-5xl font-bold bg-gradient-to-r from-blue-400 to-purple-400 bg-clip-text text-transparent mb-2 md:mb-3">
            CHENPrime
          </h1>
          <p class="text-lg md:text-xl text-slate-300 mb-1 md:mb-2">全栈开发工程师</p>
          <p class="text-sm md:text-base text-slate-400 mb-4 md:mb-4">专注于现代化 Web 开发与用户体验</p>
          
          <!-- 社交链接（胶囊形状） -->
          <div class="flex flex-wrap justify-center md:justify-start gap-2 md:gap-3 mb-3 md:mb-4">
            <a 
              v-for="social in socialLinks" 
              :key="social.name"
              @click="openNewTab(social.link)"
              class="group flex items-center gap-1.5 md:gap-2 px-3 md:px-4 py-1.5 md:py-2 bg-white/10 backdrop-blur-sm rounded-full border border-white/20 hover:bg-white/20 transition-all duration-300 hover:scale-105 hover:border-white/40"
              :title="social.name"
            >
              <span class="text-xs md:text-sm">{{ social.icon }}</span>
              <span class="text-xs md:text-sm font-medium text-slate-300 group-hover:text-white transition-colors">{{ social.name }}</span>
            </a>
          </div>
          
          <!-- 技能标签（移动端简化版） -->
          <div class="block md:hidden">
            <div class="flex flex-wrap justify-center gap-2">
              <span 
                v-for="(skill, index) in skills.slice(0, 2)" 
                :key="skill.name"
                :class="`px-3 py-1 ${skill.bgColor} ${skill.textColor} rounded-full text-xs transition-all duration-300`"
              >
                {{ skill.name }}
              </span>
              <span 
                v-if="skills.length > 2"
                class="px-3 py-1 bg-slate-500/20 text-slate-300 rounded-full text-xs cursor-pointer hover:bg-slate-500/30 transition-colors"
                :title="skills.slice(2).map(s => s.name).join(', ')"
              >
                +{{ skills.length - 2 }}更多
              </span>
            </div>
          </div>
          
          <!-- 技能标签（桌面端完整版） -->
          <div class="hidden md:flex flex-wrap justify-center md:justify-start gap-3">
            <span 
              v-for="skill in skills" 
              :key="skill.name"
              :class="`px-4 py-2 ${skill.bgColor} ${skill.textColor} rounded-full text-sm transition-all duration-300 hover:scale-105`"
            >
              {{ skill.name }}
            </span>
          </div>
        </div>
      </div>
    </header>

    <!-- 主要服务入口区域 (75% 高度) -->
    <main class="h-auto px-4 md:px-12 py-3 md:py-6">
      <div class="h-full max-w-7xl mx-auto">
        <!-- 服务卡片网格 -->
        <div class="grid grid-cols-2 md:grid-cols-4 gap-3 md:gap-6 h-full">
          <div 
            v-for="service in services" 
            :key="service.id"
            class="group relative bg-white/10 backdrop-blur-sm rounded-xl md:rounded-2xl p-3 md:p-6 cursor-pointer transition-all duration-300 hover:scale-105 hover:bg-white/20 border border-white/20"
            @auxclick="openNewTab(service.link)"
            @click="openNewTab(service.link)"
          >
            <!-- 渐变背景 -->
            <div :class="`absolute inset-0 bg-gradient-to-br ${service.color} opacity-0 group-hover:opacity-20 rounded-xl md:rounded-2xl transition-opacity duration-300`"></div>
            
            <!-- 卡片内容 -->
            <div class="relative z-10 h-full flex flex-col justify-center items-center text-center">
              <div class="text-2xl md:text-4xl mb-2 md:mb-4">{{ service.icon }}</div>
              <h3 class="font-semibold text-sm md:text-base mb-1 md:mb-2">{{ service.title }}</h3>
              <p class="text-xs md:text-sm text-slate-400 leading-relaxed">{{ service.description }}</p>
            </div>
            
            <!-- 悬停效果指示器 -->
            <div class="absolute top-2 right-2 md:top-3 md:right-3 opacity-0 group-hover:opacity-100 transition-opacity duration-300">
              <div class="w-1.5 h-1.5 md:w-2 md:h-2 bg-white rounded-full"></div>
            </div>
          </div>
        </div>
      </div>
    </main>

    <!-- 底部版权区域 -->
    <footer class="h-auto flex items-center justify-center px-4 md:px-12 py-2 md:py-4">
      <div class="text-center">
        <!-- 版权信息 -->
        <p class="text-xs md:text-sm text-slate-500">
          © 2025 CHENPrime. 用心打造每一个产品
        </p>
      </div>
    </footer>

    <!-- 背景装饰 -->
    <div class="fixed inset-0 pointer-events-none">
      <div class="absolute top-1/4 left-1/4 w-64 h-64 bg-blue-500/10 rounded-full blur-3xl"></div>
      <div class="absolute bottom-1/4 right-1/4 w-64 h-64 bg-purple-500/10 rounded-full blur-3xl"></div>
    </div>
  </div>
</template>

<style scoped>
/* 确保页面不会出现滚动条 */
html, body {
  overflow: hidden;
}

/* 自定义滚动条样式（如果需要） */
::-webkit-scrollbar {
  display: none;
}

/* 响应式调整 */
@media (max-width: 768px) {
  /* 移动端确保垂直居中布局 */
  header {
    justify-content: center !important;
  }
  
  header > div {
    align-items: center !important;
    text-align: center !important;
  }
}

@media (min-width: 769px) {
  /* 桌面端确保水平居中布局 */
  header > div {
    flex-direction: row !important;
    align-items: center !important;
    justify-content: center !important;
  }
}

@media (max-width: 480px) {
  /* 超小屏幕优化 */
  .grid {
    gap: 0.5rem;
  }
  
  header {
    padding: 0.75rem;
    height: auto !important;
    min-height: 25vh;
  }
  
  main {
    padding: 0.75rem;
    height: auto !important;
  }
  
  footer {
    padding: 0.5rem;
    height: auto !important;
    min-height: 10vh;
  }
}
</style>
