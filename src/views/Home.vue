<template>
  <div class="home-container">
    <!-- 1. 导航栏组件 -->
    <NavBar />
    
    <!-- 2. 平台名称模块 -->
     <div class="platform-banner">
      <div class="banner-content">
        <div class="platform-title">
          <img src="@/assets/icons/book5.svg" alt="Book Icon" class="book-icon">
          <h1>EduPlatform</h1>
        </div>
        <p>精选优质课程，更新前沿资讯，配备分类题库，打造个人学习可视化平台，助力你的大学生涯。</p>
      </div>
    </div>


    <!-- 3. 主要内容区域 -->
    <div class="content-wrapper">
      <!-- 3.1 课程模块 (左侧) -->
      <div class="course-section">
        <h2 class="section-title">课程推荐</h2>
        <div class="course-cards">
          <div 
            class="course-card" 
            v-for="course in courses" 
            :key="course.id"
            @click="goToCourse(course.id)"
          >
            <div class="course-header">
              <span class="course-university">{{ course.university }}</span>
            </div>
            <div class="course-title">{{ course.title }}</div>
            <div class="course-footer">
              <span class="course-teacher">{{ course.teacher }}</span>
            </div>
          </div>
        </div>
      </div>
      
      <!-- 3.2 资讯模块 (右侧) -->
      <div class="news-section">
        <h2 class="section-title">资讯推荐</h2>
        <div class="news-list">
          <div 
            class="news-item" 
            v-for="news in newsList" 
            :key="news.id"
            @click="goToNews(news.id)"
          >
            <div class="news-title">{{ news.title }}</div>
            <div class="news-content">{{ news.content }}</div>
            <div class="news-divider" v-if="!news.last"></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import NavBar from '../components/NavBar.vue'
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

// 课程数据
const courses = ref([
  {
    id: 1,
    title: '网络技术与应用',
    university: '南京邮电大学',
    teacher: '张教授'
  },
  {
    id: 2,
    title: 'Python数据获取与可视化',
    university: '南华大学',
    teacher: '李教授'
  },
  {
    id: 3,
    title: '大数据导论-大数据如何改变世界',
    university: '北京理工大学',
    teacher: '王教授'
  },
  {
    id: 4,
    title: '大数据分析',
    university: '清华大学',
    teacher: '赵教授'
  }
])

// 资讯数据
const newsList = ref([
  {
    id: 1,
    title: '中国新能源企业加速海外建厂 提升供应链韧性',
    content: '水利部针对重庆四川甘肃启动洪水防御IV级应急响应',
    last: false
  },
  {
    id: 2,
    title: '中国有数 | 1.85亿里藏着中国的烟火气与硬实力',
    content: '事关网络身份认证、征信服务收费等7月这些新规格施行',
    last: false
  },
  {
    id: 3,
    title: '中国引领智能绿色转型，合作是唯一通路',
    content: '商务部就美与有关国家关税谈判情况答记者问',
    last: true
  }
])

const goToCourse = (id) => {
  // 实际开发中替换为你的课程详情页路由
  console.log('跳转到课程:', id)
  // router.push(`/course/${id}`)
}

const goToNews = (id) => {
  // 实际开发中替换为你的资讯详情页路由
  console.log('跳转到资讯:', id)
  // router.push(`/news/${id}`)
}
</script>

<style scoped>
/* 平台名称模块 - 修改为横幅样式 */
.platform-banner {
  height: 280px;
  background: linear-gradient(135deg,rgb(49, 125, 201),rgb(85, 73, 215));
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  position: relative;
  overflow: hidden;
}

.banner-content {
  text-align: center;
  z-index: 2;
  max-width: 800px;
  padding: 0 20px;
}


.platform-title {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 15px;
}

.book-icon {
  width: 50px;
  height: 50px;
  margin-right: 20px;
 
}

.platform-title h1 {
  font-size: 42px;
  text-shadow: 0 2px 4px rgba(0,0,0,0.2);
  margin: 5px; /* 移除默认的h1 margin */
}

.platform-banner p {
  font-size: 17px;
  margin-bottom: 25px;
  opacity: 0.9;
}

.platform-banner::before {
  content: '';
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: radial-gradient(circle, rgba(255,255,255,0.1) 0%, rgba(255,255,255,0) 70%);
  z-index: 1;
}

/* 主要内容区域样式 */
.home-container {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.content-wrapper {
  display: flex;
  flex: 1;
  padding: 30px;
  gap: 30px;
}

.section-title {
  font-size: 15px;
  font-weight: 600;
  margin-bottom: 20px;
  color: #333;
  padding-bottom: 10px;
  border-bottom: 2px solid #eee;
}

/* 课程模块样式 */
.course-section {
  flex: 2;
  padding: 20px;
  border-radius: 8px;
  background: #fff;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
}

.course-cards {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 20px;
}

.course-card {
  background: #fff;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  transition: all 0.3s ease;
  border: 1px solid #eee;
}

.course-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
}

.course-header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 15px;
}

.course-university {
  font-size: 14px;
  color: #666;
  font-weight: 500;
}

.course-title {
  font-size: 18px;
  font-weight: 600;
  color: #333;
  margin-bottom: 15px;
  line-height: 1.4;
}

.course-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.course-teacher {
  font-size: 14px;
  color: #888;
}

/* 资讯模块样式 */
.news-section {
  flex: 1;
  padding: 20px;
  border-radius: 8px;
  background: #fff;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
}

.news-list {
  display: flex;
  flex-direction: column;
}

.news-item {
  padding: 15px 0;
  cursor: pointer;
}

.news-item:hover .news-title {
  color: #409EFF;
}

.news-title {
  font-size: 16px;
  font-weight: 600;
  color: #333;
  margin-bottom: 8px;
  transition: color 0.3s;
}

.news-content {
  font-size: 14px;
  color: #666;
  line-height: 1.5;
}

.news-divider {
  height: 1px;
  background: #eee;
  margin: 15px 0;
}
</style>
