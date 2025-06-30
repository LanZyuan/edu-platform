<template>
  <div class="profile-page">
    <!-- 顶部导航栏 -->
    <NavBar />

    <div class="main-container">
      <!-- 个人信息区域 -->
      <div class="profile-section">
        <div class="avatar-container">
          <img src="@/assets/icons/avatar.svg" alt="用户头像" class="avatar">
        </div>
        <div class="info-container">
          <h1 class="username">张三</h1>
          <div class="info-grid">
            <div class="info-item">
              <span class="info-label">专业：</span>
              <span class="info-value">计算机科学与技术</span>
            </div>
            <div class="info-item">
              <span class="info-label">年级：</span>
              <span class="info-value">大三</span>
            </div>
            <div class="info-item">
              <span class="info-label">学号：</span>
              <span class="info-value">20210001</span>
            </div>
            <div class="info-item">
              <span class="info-label">邮箱：</span>
              <span class="info-value">zhangsan@example.com</span>
            </div>
          </div>
        </div>
      </div>

      <!-- 选项卡区域 -->
      <div class="tab-section">
        <div class="tab-buttons">
          <button
              v-for="tab in tabs"
              :key="tab.id"
              :class="['tab-button', { active: activeTab === tab.id }]"
              @click="activeTab = tab.id"
          >
            <span class="button-icon">{{ getIcon(tab.id) }}</span>
            <span class="button-text">{{ tab.name }}</span>
          </button>
        </div>

        <!-- 动态内容区域 -->
        <div class="tab-content">
          <component :is="activeTabComponent" />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import NavBar from '@/components/NavBar.vue';
import CourseCollection from '@/components/CourseCollection.vue';
import WrongQuestionBook from '@/components/WrongQuestionBook.vue';
import StudyProgress from '@/components/StudyProgress.vue';
import AcademicAnalysis from '@/components/AcademicAnalysis.vue';

// 选项卡配置
const tabs = [
  { id: 'courseCollection', name: '课程收藏' },
  { id: 'wrongQuestionBook', name: '错题本' },
  { id: 'studyProgress', name: '个人修读情况' },
  { id: 'academicAnalysis', name: '学业分析' }
];

// 当前激活的选项卡
const activeTab = ref('courseCollection');

// 计算当前显示的组件
const activeTabComponent = computed(() => {
  switch (activeTab.value) {
    case 'courseCollection': return CourseCollection;
    case 'wrongQuestionBook': return WrongQuestionBook;
    case 'studyProgress': return StudyProgress;
    case 'academicAnalysis': return AcademicAnalysis;
    default: return CourseCollection;
  }
});

// 为按钮添加图标
const getIcon = (tabId) => {
  const icons = {
    courseCollection: '📚',
    wrongQuestionBook: '❌',
    studyProgress: '📊',
    academicAnalysis: '🔍'
  };
  return icons[tabId] || '●';
};
</script>

<style scoped>
.profile-page {
  background-color: #f8fafc;
  min-height: 100vh;
  padding-bottom: 50px;
}

.main-container {
  max-width: 1500px;
  margin: 0 auto;
  padding: 0 30px;
}

/* 个人信息区域样式 */
.profile-section {
  display: flex;
  margin-top: 40px;
  padding: 40px;
  background-color: #fff;
  border-radius: 16px;
  box-shadow: 0 6px 25px rgba(0, 0, 0, 0.08);
}

.avatar-container {
  margin-right: 50px;
  display: flex;
  align-items: center;
}

.avatar {
  width: 200px;
  height: 200px;
  border-radius: 50%;
  object-fit: cover;
  border: 4px solid #f0f8ff;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
}

.info-container {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.username {
  font-size: 42px;
  margin-bottom: 25px;
  color: #1a2b50;
  font-weight: 600;
}

.info-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px 40px;
}

.info-item {
  display: flex;
  align-items: center;
}

.info-label {
  font-size: 22px;
  color: #4a5568;
  font-weight: 500;
  min-width: 80px;
}

.info-value {
  font-size: 24px;
  color: #2d3748;
  font-weight: 500;
}

/* 选项卡样式 */
.tab-section {
  margin-top: 50px;
}

.tab-buttons {
  display: flex;
  border-bottom: 3px solid #e2e8f0;
  background-color: #fff;
  border-radius: 12px 12px 0 0;
  overflow: hidden;
}

.tab-button {
  flex: 1;
  padding: 25px 0;
  background: none;
  border: none;
  font-size: 24px;
  cursor: pointer;
  color: #4a5568;
  transition: all 0.3s ease;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 15px;
}

.tab-button:hover {
  color: #2b6cb0;
  background-color: #f7fafc;
}

.tab-button.active {
  color: #2b6cb0;
  font-weight: 600;
}

.tab-button.active::after {
  content: '';
  position: absolute;
  bottom: -3px;
  left: 0;
  right: 0;
  height: 5px;
  background-color: #2b6cb0;
}

.button-icon {
  font-size: 28px;
}

.tab-content {
  padding: 50px;
  background-color: #fff;
  border-radius: 0 0 16px 16px;
  box-shadow: 0 6px 25px rgba(0, 0, 0, 0.05);
  min-height: 500px;
  font-size: 20px;
  line-height: 1.8;
}

/* 响应式调整 */
@media (max-width: 1200px) {
  .profile-section {
    flex-direction: column;
    align-items: center;
    text-align: center;
    padding: 30px;
  }

  .avatar-container {
    margin-right: 0;
    margin-bottom: 30px;
  }

  .info-grid {
    grid-template-columns: 1fr;
    gap: 15px;
  }

  .info-item {
    justify-content: center;
    flex-direction: column;
  }

  .tab-buttons {
    flex-wrap: wrap;
  }

  .tab-button {
    flex: 1 0 45%;
    padding: 20px 0;
    font-size: 20px;
  }
}

@media (max-width: 768px) {
  .main-container {
    padding: 0 20px;
  }

  .avatar {
    width: 160px;
    height: 160px;
  }

  .username {
    font-size: 32px;
  }

  .info-label,
  .info-value {
    font-size: 18px;
  }

  .tab-button {
    flex: 1 0 100%;
    padding: 18px 0;
    font-size: 20px;
  }

  .tab-content {
    padding: 30px;
    min-height: 400px;
  }
}
</style>
