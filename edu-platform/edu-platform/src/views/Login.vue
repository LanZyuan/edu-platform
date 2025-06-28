<template>
  <div class="login-container">
    <h1>在线教育平台登录</h1>
    <form @submit.prevent="handleLogin">
      <div>
        <label>用户名：</label>
        <input type="text" v-model="username" required>
      </div>
      <div>
        <label>密码：</label>
        <input type="password" v-model="password" required>
      </div>
      <button type="submit">登录</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const username = ref('')
const password = ref('')
const router = useRouter()

const handleLogin = () => {
  // 实际项目这里调用API
  console.log('登录信息:', username.value, password.value)
  
  // 模拟登录成功
  localStorage.setItem('isAuthenticated', 'true')
  router.push('/home')
}
</script>

<style scoped>
.login-container {
  max-width: 400px;
  margin: 100px auto;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
}
input {
  margin: 10px 0;
  padding: 8px;
  width: 100%;
}
button {
  padding: 10px 15px;
  background: #42b983;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
</style>.