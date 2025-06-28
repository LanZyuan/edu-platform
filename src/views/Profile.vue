<template>
  <div class="profile-container">
    <h1>个人信息</h1>
    <div class="profile-card">
      <div class="avatar">
        <img :src="user.avatar" alt="用户头像">
      </div>
      <div class="info">
        <p><strong>姓名：</strong>{{ user.name }}</p>
        <p><strong>邮箱：</strong>{{ user.email }}</p>
        <p><strong>注册时间：</strong>{{ user.joinDate }}</p>
      </div>
      <button @click="goBack">返回首页</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

// 模拟用户数据
const user = ref({
  name: '张三',
  email: 'zhangsan@example.com',
  avatar: 'https://cube.elemecdn.com/0/88/03b0d39583f48206768a7534e55bcpng.png',
  joinDate: '2023-01-15'
})

const goBack = () => {
  router.push('/home')
}
</script>

<style scoped>
.profile-container {
  max-width: 600px;
  margin: 50px auto;
  padding: 20px;
}

.profile-card {
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 20px;
  margin-top: 20px;
  position: relative;
}

.avatar img {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  border: 2px solid #42b983;
}

.info {
  margin: 20px 0;
}

button {
  padding: 8px 16px;
  background: #42b983;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
</style>