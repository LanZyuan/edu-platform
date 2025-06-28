<template>
  <div class="login-page">
    <div class="platform-info">
      <h1 class="platform-name">EduPlatform</h1>
      <p class="platform-slogan">智慧教育 · 未来学习</p>
      <div class="education-icons">
        <i class="fas fa-book-open"></i>
        <i class="fas fa-graduation-cap"></i>
        <i class="fas fa-laptop-code"></i>
        <i class="fas fa-atom"></i>
      </div>
    </div>
    
    <div class="login-wrapper">
      <div class="login-container">
        <h2 class="login-title">用户登录</h2>
        <form @submit.prevent="handleLogin" class="login-form">
          <div class="form-row">
            <span class="input-label">用户名：</span>
            <input 
              type="text" 
              v-model="username" 
              placeholder="请输入用户名"
              required
              class="form-input"
            >
          </div>
          <div class="form-row">
            <span class="input-label">密码：</span>
            <input 
              type="password" 
              v-model="password" 
              placeholder="请输入密码"
              required
              class="form-input"
            >
          </div>
          <div class="remember-row">
            <label class="remember-me">
              <input type="checkbox"> 记住密码
            </label>
          </div>
          <button type="submit" class="login-btn">登录</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const username = ref('')
const password = ref('')
const router = useRouter()

const handleLogin = () => {
  console.log('登录信息:', username.value, password.value)
  localStorage.setItem('isAuthenticated', 'true')
  router.push('/home')
}
</script>

<style scoped>
.login-page {
  display: flex;
  min-height: 100vh;
  background: linear-gradient(135deg, #1976d2, #2196f3);
  padding-top: 40px; /* 调整整体下移距离 */
}

.platform-info {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: flex-start; /* 改为flex-start使内容上移 */
  align-items: center;
  color: white;
  padding: 2rem;
  padding-top: 1rem; /* 减少顶部内边距使内容更高 */
}

.platform-name {
  font-size: 2.8rem;
  font-weight: bold;
  margin-bottom: 0.8rem; /* 减小下边距 */
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.platform-slogan {
  font-size: 1.4rem;
  opacity: 0.9;
  margin-bottom: 1.5rem; /* 增加下边距为图标留空间 */
}

/* 新增教育图标样式 */
.education-icons {
  display: flex;
  justify-content: center;
  gap: 30px; /* 图标间距 */
  margin-top: 1rem;
  font-size: 2rem;
  color: rgba(255, 255, 255, 0.7);
  animation: float 3s ease-in-out infinite;
}

.education-icons i {
  animation: float 3s ease-in-out infinite;
  animation-delay: calc(var(--i) * 0.2s);
}

@keyframes float {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

.login-wrapper {
  width: 500px;
  display: flex;
  align-items: center;
  padding-right: 10%;
  margin-left: -30px;
}

.login-container {
  width: 100%;
  background: white;
  padding: 2rem;
  border-radius: 8px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
}

.login-title {
  font-size: 1.5rem;
  color: #333;
  margin-bottom: 1.5rem;
  text-align: center;
  font-weight: 500;
}

.login-form {
  width: 100%;
}

.form-row {
  display: flex;
  align-items: center;
  margin-bottom: 1.2rem;
  white-space: nowrap;
}

.input-label {
  display: inline-block;
  width: auto;
  color: #666;
  font-size: 1rem;
  margin-right: 12px;
  line-height: 1.5;
}

.form-input {
  flex: 1;
  padding: 0.8rem 1rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 1rem;
  min-width: 0;
}

.form-input:focus {
  border-color: #2196f3;
  outline: none;
  box-shadow: 0 0 0 2px rgba(33, 150, 243, 0.2);
}

.remember-row {
  margin: 1.5rem 0;
}

.remember-me {
  display: flex;
  align-items: center;
  font-size: 0.95rem;
  color: #666;
  cursor: pointer;
}

.remember-me input {
  margin-right: 8px;
  width: 16px;
  height: 16px;
}

.login-btn {
  width: 100%;
  padding: 0.9rem;
  background: #2196f3;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 1.1rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.3s;
}

.login-btn:hover {
  background: #1a80d6;
}

@media (max-width: 768px) {
  .login-page {
    flex-direction: column;
    padding-top: 20px;
  }
  
  .platform-info {
    padding: 1rem;
    text-align: center;
  }
  
  .education-icons {
    gap: 20px;
    font-size: 1.5rem;
  }
  
  .login-wrapper {
    width: 90%;
    padding: 0;
    margin: 0 auto 2rem;
  }
  
  .login-container {
    padding: 1.5rem;
  }
  
  .form-row {
    flex-direction: column;
    align-items: flex-start;
  }
  
  .input-label {
    margin-bottom: 0.5rem;
    margin-right: 0;
  }
}
</style>