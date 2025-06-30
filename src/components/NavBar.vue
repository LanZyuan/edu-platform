<template>
  <header class="navbar">
    <!-- 左侧导航按钮 -->
    <div class="left-buttons">
      <div 
        class="nav-item" 
        v-for="button in leftButtons" 
        :key="button.name"
        @mouseenter="showDropdown(button.route)"
        @mouseleave="hideDropdown(button.route)"
      >
        <button
          @click="navigateTo(button.route)"
          :class="{ active: activeButton === button.route }"
        >
          {{ button.name }}
          <img src="@/assets/icons/th.svg" class="dropdown-icon" alt="下拉菜单">
        </button>
        
        <!-- 下拉菜单 -->
        <div 
          v-if="activeDropdown === button.route" 
          class="dropdown-menu"
          @mouseenter="showDropdown(button.route)"
          @mouseleave="hideDropdown(button.route)"
        >
          <div 
            class="dropdown-item" 
            v-for="item in getDropdownItems(button.route)" 
            :key="item.name"
            @click="navigateToSub(item.route)"
          >
            {{ item.name }}
          </div>
        </div>
      </div>
    </div>

    <!-- 中间搜索框 -->
    <div class="search-container">
      <div class="search-box">
        <input 
          type="text" 
          placeholder="搜索课程、资讯..." 
          class="search-input"
          v-model="searchQuery"
          @keyup.enter="handleSearch"
        >
        <button class="search-button" @click="handleSearch">
          <img src="@/assets/icons/search1.svg" class="search-icon" alt="搜索">
        </button>
      </div>
    </div>

       <!-- 右侧用户信息 -->
    <div class="user-info" @click="toggleDropdown">
      <img :src="user.avatar" alt="用户头像" class="avatar">
      <span class="username">{{ user.name }}</span>
      
      <!-- 用户下拉菜单 -->
      <div v-if="showUserDropdown" class="dropdown-menu">
        <div class="dropdown-item" @click="goToProfile">
          个人中心
        </div>
        <div class="dropdown-item" @click="handleLogout">
          退出登录
        </div>
      </div>
    </div>
  </header>
</template>

<script setup>
import { ref, reactive } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const showUserDropdown = ref(false)
const activeDropdown = ref(null)
const activeButton = ref(null)
const searchQuery = ref('')
let hideTimeout = null

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

// 下拉菜单项配置
const dropdownItems = {
  '/courses': [
    { name: '个性化课程', route: '/courses/personalized' },
    { name: '专业热门课程', route: '/courses/popular' },
    { name: '升学考研专区', route: '/courses/postgraduate' }
  ],
  '/news': [
    { name: '学术期刊', route: '/news/journals' },
    { name: '竞赛信息', route: '/news/competitions' },
    { name: '教学活动', route: '/news/activities' },
    { name: '研究生招生', route: '/news/admissions' }
  ],
  '/questions': [
    { name: '英语四六级题库', route: '/questions/cet' },
    { name: '专业课程', route: '/questions/major' },
    { name: '考研题库', route: '/questions/postgraduate' }
  ]
}

// 搜索处理
const handleSearch = () => {
  if (searchQuery.value.trim()) {
    router.push(`/search?q=${encodeURIComponent(searchQuery.value)}`)
    searchQuery.value = ''
  }
}

// 获取对应路由的下拉菜单项
const getDropdownItems = (route) => {
  return dropdownItems[route] || []
}

// 显示下拉菜单
const showDropdown = (route) => {
  clearTimeout(hideTimeout)
  activeDropdown.value = route
}

// 隐藏下拉菜单（延迟300ms）
const hideDropdown = (route) => {
  hideTimeout = setTimeout(() => {
    if (activeDropdown.value === route) {
      activeDropdown.value = null
    }
  }, 300)
}

// 导航到指定路由
const navigateTo = (route) => {
  activeButton.value = route
  router.push(route)
}

// 导航到子路由
const navigateToSub = (route) => {
  router.push(route)
  activeDropdown.value = null
}

// 切换用户下拉菜单显示状态
const toggleDropdown = () => {
  showUserDropdown.value = !showUserDropdown.value
}

// 跳转到个人信息页
const goToProfile = () => {
  router.push('/profile')
  showUserDropdown.value = false
}

// 处理退出登录
const handleLogout = () => {
  localStorage.removeItem('isAuthenticated')
  router.push('/login')
}
</script>

<style scoped>
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 30px;
  height: 40px;
  background: #fff;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
  position: sticky;
  top: 0;
  z-index: 100;
}

.left-buttons {
  display: flex;
  gap: 20px;
}

.nav-item {
  position: relative;
  height: 100%;
  display: flex;
  align-items: center;
}

button {
  padding: 8px 16px;
  background: transparent;
  border: none;
  font-size: 15px;
  color: #333;
  cursor: pointer;
  transition: all 0.3s;
  border-radius: 4px;
  display: flex;
  align-items: center;
  gap: 6px;
  height: 100%;
}

button:hover {
  background:rgb(230, 239, 253);
}



.dropdown-icon {
  width: 16px;
  height: 16px;
  opacity: 0.7;
  transition: transform 0.2s;
}

.nav-item:hover .dropdown-icon {
  opacity: 1;
  transform: rotate(180deg);
}

/* 搜索框样式 */
.search-container {
  flex: 1;
  max-width: 400px;
  margin: 0 -200px 0 200px;
}

.search-box {
  position: relative;
  width: 100%;
  max-width: 320px;
  margin: 0 auto;
}

.search-input {
  width: 100%;
  padding: 8px 40px 8px 15px;
  border: 1.4px solid #b0b0b0; /* 进一步加深边框颜色 */
  border-radius: 20px;
  font-size: 14px;
  transition: all 0.3s;
  outline: none;
}

.search-input:hover {
  border-color:rgb(66, 121, 185);
  box-shadow: 0 0 0 2px rgba(81, 135, 211, 0.46);
}

.search-button {
  position: absolute;
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
  background: none;
  border: none;
  cursor: pointer;
  padding: 5px;
}

.search-icon {
  width: 16px;
  height: 16px;
  opacity: 0.6;
  transition: opacity 0.2s;
}

.search-button:hover .search-icon {
  opacity: 1;
}

/* 用户信息样式 */
.user-info {
  display: flex;
  align-items: center;
  gap: 10px;
  cursor: pointer;
  padding: 5px 10px;
  border-radius: 20px;
  transition: background 0.3s;
  position: relative;
  height: 100%;
}

.user-info:hover {
  background: #f5f7fa;
}

.avatar {
  width: 36px;
  height: 36px;
  border-radius: 50%;
  object-fit: cover;
  border: 2px solid #f0f0f0;
}

.username {
  font-size: 14px;
  font-weight: 500;
  color: #333;
}

/* 下拉菜单通用样式 */
.dropdown-menu {
  position: absolute;
  top: 100%;
  left: 0;
  background: white;
  border-radius: 6px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  min-width: 160px;
  z-index: 1000;
  margin-top: 5px;
  overflow: hidden;
 
}

.user-dropdown {
  right: 0;
  left: auto;
}

.dropdown-item {
  padding: 8px 16px;
  font-size: 14px;
  color: #333;
  transition: all 0.2s;
  display: flex;
  align-items: center;
  gap: 8px;
}

.dropdown-item:hover {
  background:rgb(206, 221, 243);
  color:rgb(66, 121, 185);
}

.dropdown-item .dropdown-icon {
  width: 14px;
  height: 14px;
  opacity: 0.8;
}


</style>