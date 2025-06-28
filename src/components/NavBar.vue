 <template>
  <header class="navbar">
    <!-- 左侧导航按钮 -->
    <div class="left-buttons">
      <button
        v-for="button in leftButtons"
        :key="button.name"
        @click="navigateTo(button.route)"
        :class="{ active: activeButton === button.route }"
      >
        {{ button.name }}
      </button>
    </div>

    <!-- 右侧用户信息 -->
    <div class="user-info" @click="goToProfile">
      <img :src="user.avatar" alt="用户头像" class="avatar">
      <span class="username">{{ user.name }}</span>
    </div>
  </header>
</template>

<script setup>
import { ref, reactive } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

// 模拟用户数据
const user = reactive({
  name: '张三',
  avatar: 'https://cube.elemecdn.com/0/88/03b0d39583f48206768a7534e55bcpng.png'
})

// 左侧按钮配置
const leftButtons = ref([
  { name: '课程学习', route: '/courses' },
  { name: '资讯', route: '/news' },
  { name: '题库', route: '/questions' }
])

// 当前激活的按钮（根据路由高亮）
const activeButton = ref(router.currentRoute.value.path)

// 导航到指定路由
const navigateTo = (route) => {
  // 实际项目中这里会跳转到对应页面
  // 这里我们只做模拟，更新激活状态
  activeButton.value = route
  alert(`即将跳转到: ${route}`)
}

// 跳转到个人信息页
const goToProfile = () => {
  router.push('/profile')
}
</script>

<style scoped>
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px 30px;
  background: #fff;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  position: sticky;
  top: 0;
  z-index: 100;
}

.left-buttons {
  display: flex;
  gap: 20px;
}

button {
  padding: 8px 16px;
  background: transparent;
  border: none;
  font-size: 16px;
  cursor: pointer;
  transition: all 0.3s;
  border-radius: 4px;
}

button:hover {
  background: #f5f7fa;
}

button.active {
  background: #42b983;
  color: white;
}

.user-info {
  display: flex;
  align-items: center;
  gap: 10px;
  cursor: pointer;
  padding: 5px 10px;
  border-radius: 20px;
  transition: background 0.3s;
}

.user-info:hover {
  background: #f5f7fa;
}

.avatar {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  border: 2px solid #e6e6e6;
}

.username {
  font-weight: 500;
}
</style>

<template>
  <div class="nav-container">
    <!-- 标题元素 -->
    <div
        class="nav-title"
        @mouseover="showOptions = true"
        @mouseleave="showOptions = false"
    >
      我的标题
      <!-- 下拉选项 -->
      <div
          v-show="showOptions"
          class="options-container"
          @mouseover="showOptions = true"
      >
        <div class="option-item">选项一</div>
        <div class="option-item">选项二</div>
        <div class="option-item">选项三</div>
        <div class="option-item">选项四</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showOptions: false // 控制选项显示状态
    }
  }
}
</script>

<style scoped>
.nav-container {
  position: relative;
  font-family: 'Arial', sans-serif;
}

.nav-title {
  padding: 12px 20px;
  background-color: #3498db;
  color: white;
  cursor: pointer;
  border-radius: 4px;
  position: relative;
  display: inline-block;
  transition: background-color 0.3s;
}

.nav-title:hover {
  background-color: #2980b9;
}

.options-container {
  position: absolute;
  top: 100%;
  left: 0;
  width: 150px;
  background-color: white;
  border: 1px solid #ddd;
  border-radius: 4px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  z-index: 100;
  margin-top: 5px;
  animation: fadeIn 0.3s ease;
}

.option-item {
  padding: 10px 15px;
  border-bottom: 1px solid #eee;
  transition: background-color 0.2s;
}

.option-item:last-child {
  border-bottom: none;
}

.option-item:hover {
  background-color: #f5f5f5;
  color: #3498db;
}

/* 淡入动画 */
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>