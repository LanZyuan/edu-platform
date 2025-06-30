<template>
  <div class="login-page">
    <div class="white-edge"></div>
    <div class="platform-info">
      <h1 class="platform-name">EduPlatform</h1>
      <p class="platform-slogan">智慧教育 · 未来学习</p>
      <div class="login-icon-container">
        <img src="@/assets/icons/login.svg" alt="Login Icon" class="login-icon">
      </div>
    </div>
    
    <div class="login-wrapper">
      <div class="login-border">
        <div class="login-container">
          <h2 class="login-title">用户登录</h2>
          <form @submit.prevent="handleLogin" class="login-form">
            <div class="form-row">
              <span class="input-label">学号：</span>
              <input 
                type="text" 
                v-model="studentId" 
                placeholder="请输入学号"
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
            <button type="submit" class="login-btn" :disabled="loading">
              {{ loading ? '登录中...' : '登录' }}
            </button>
            <div class="remember-row">
              <label class="remember-me">
                <input type="checkbox"> 记住密码
              </label>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
 
  <!-- 添加提示框 -->
  <div v-if="showErrorModal" class="error-modal">
    <div class="modal-content">
      <span class="close" @click="showErrorModal = false">&times;</span>
      <p>{{ errorMessage }}</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import axios from 'axios'

const studentId = ref('')
const password = ref('')
const showErrorModal = ref(false)
const errorMessage = ref('')
const loading = ref(false)
const router = useRouter()


const handleLogin = async () => {
  loading.value = true
  
  try {
    const response = await axios.post('http://10.242.33.86:8081/api/login', {
      studentId: studentId.value,
      password: password.value
    })

    console.log('API Response:', response.data) // 添加调试日志

    if (response.data.code === 200) {
      // 确保这里的结构与API返回的结构一致
      const token = response.data.token || response.data.data?.token
      const userData = response.data.data || {}
      
      if (!token) {
        throw new Error('Token not found in response')
      }

      // 存储token和用户信息
      localStorage.setItem('token', token)
      localStorage.setItem('userInfo', JSON.stringify(userData))
      
      // 设置axios全局授权头
      axios.defaults.headers.common['Authorization'] = token
      
      // 添加跳转前的日志
      console.log('Login successful, redirecting to /home')
      
      // 跳转到首页
      router.push('/home').catch(err => {
        console.error('Router push error:', err)
      })
    } else {
      errorMessage.value = response.data.message || '登录失败'
      showErrorModal.value = true
    }
  } catch (error) {
    console.error('Login error:', error)
    if (error.response) {
      errorMessage.value = error.response.data?.message || '登录失败'
    } else {
      errorMessage.value = error.message || '网络错误，请稍后重试'
    }
    showErrorModal.value = true
  } finally {
    loading.value = false
  }
}
</script>

<style scoped>
/* 保持原有样式不变 */
.white-edge {
  position: fixed;
  left: 0;
  top: 0;
  width: 3.8cm;
  height: 100vh;
  background:  linear-gradient(135deg,rgb(87, 156, 216),rgb(138, 178, 227));
}

.login-page {
  display: flex;
  min-height: 100vh;
  background: linear-gradient(135deg, #1976d2, #2196f3);
  padding-top: 40px;
  padding-left: 1cm;
}

.platform-info {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  color: white;
  padding: 2rem;
  padding-top: 4rem;
  margin-left: 1cm;
  position: relative;
}

.platform-name {
  font-size: 3.2rem;
  font-weight: bold;
  margin-bottom: 0.8rem;
  text-shadow: 0 2px 4px rgba(8, 5, 5, 0.1);
  letter-spacing: 0.3rem;
}

@keyframes float {
  0% {
    transform: translateY(0);
    text-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  }
  50% {
    transform: translateY(-17px);
    text-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
  }
  100% {
    transform: translateY(0);
    text-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  }
}

.platform-slogan {
  font-size: 1.3rem;
  opacity: 0.9;
  margin-bottom: 1.5rem;
}

.login-wrapper {
  width: 450px;
  display: flex;
  align-items: center;
  padding-right: 10%;
  margin-left: -30px;
}

.login-border {
  width: 100%;
  padding: 10px;
  background-color: rgba(192, 217, 232, 0.5);
  border-radius: 5px;
  backdrop-filter: blur(5px);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
  transform: scale(1);
}

.login-border:hover {
  transform: scale(1.02);
  box-shadow: 0 6px 25px rgba(0, 0, 0, 0.15);
}

.login-container {
  width: 100%;
  background: white;
  padding: 2rem;
  border-radius: 8px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

.login-title {
  font-size: 1.2rem;
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
  font-size: 0.9rem;
  margin-right: 12px;
  line-height: 1.5;
}

.form-input {
  flex: 1;
  padding: 0.8rem 1rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 0.85rem;
  height: 36px;        
  min-width: 0;
}

.form-input:focus {
  border-color: #2196f3;
  outline: none;
  box-shadow: 0 0 0 2px rgba(33, 150, 243, 0.2);
}

.remember-row {
  margin: 1.2rem 0;
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
  padding: 0.5rem;
  background: #2196f3;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 0.9rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.3s;
}

.login-btn:hover {
  background: #1a80d6;
}

.login-btn:disabled {
  background: #cccccc;
  cursor: not-allowed;
}

.login-icon-container {
  margin-top: 1.5rem;
  text-align: center;
}

.login-icon {
  width: 420px;
  height:420px;
  opacity: 0.9;
  transition: all 0.3s ease;
  animation: float 2.3s ease-in-out infinite;
  animation-delay: 0s;
}

.error-modal {
  position: fixed;
  z-index: 1000;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.4);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background-color: #fefefe;
  padding: 20px;
  border-radius: 8px;
  width: 300px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  position: relative;
  text-align: center;
}

.modal-content p {
  margin: 15px 0;
  color: #f44336;
  font-size: 16px;
}

.close {
  position: absolute;
  right: 10px;
  top: 5px;
  color: #aaa;
  font-size: 24px;
  font-weight: bold;
  cursor: pointer;
}

.close:hover {
  color: #333;
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
