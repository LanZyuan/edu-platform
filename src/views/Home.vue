<template>
  <div class="home-container">
    <!-- 添加导航栏 -->
    <NavBar />
    
    <div class="main-content">
      <h1>欢迎来到在线教育平台</h1>
      <p>这里是课程主页，您可以选择课程开始学习</p>
      
      <!-- 模拟课程卡片 -->
      <div class="course-card">
        <h2>Vue.js 入门教程</h2>
        <p>从零开始学习Vue框架，掌握核心概念</p>
        <button @click="startLearning">开始学习</button>
      </div>
      
      <button class="logout-btn" @click="handleLogout">退出登录</button>
    </div>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router'
import NavBar from '../components/NavBar.vue'

const router = useRouter()

const handleLogout = () => {
  localStorage.removeItem('isAuthenticated')
  router.push('/login')
}

const startLearning = () => {
  alert('开始课程学习！')
}
</script>

<style scoped>
.home-container {
  display: flex;
  flex-direction: column;
  height: 100vh;
}

.main-content {
  flex: 1;
  padding: 30px;
  text-align: center;
}

.course-card {
  max-width: 600px;
  margin: 30px auto;
  padding: 20px;
  border: 1px solid #e4e7ed;
  border-radius: 8px;
  background: #f9fafc;
  box-shadow: 0 2px 12px 0 rgba(0,0,0,0.1);
}

.course-card h2 {
  color: #42b983;
}

.logout-btn {
  padding: 10px 20px;
  background: #ff4757;
  color: white;
  border: none;
  border-radius: 4px;
  margin-top: 20px;
  cursor: pointer;
}
</style>