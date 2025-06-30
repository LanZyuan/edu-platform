<template>
  <div class="course-collection">
    <h2>课程收藏</h2>
    <p>您收藏的课程列表如下：</p>

    <div class="course-list">
      <div class="course-card">
        <h3>数据结构与算法</h3>
        <p>王教授 · 计算机学院</p>
        <div class="course-meta">
          <span>⭐ 4.8 (120评价)</span>
          <span>🕒 32课时</span>
        </div>
      </div>

      <div class="course-card">
        <h3>计算机网络原理</h3>
        <p>李教授 · 信息工程学院</p>
        <div class="course-meta">
          <span>⭐ 4.7 (95评价)</span>
          <span>🕒 28课时</span>
        </div>
      </div>

      <div class="course-card">
        <h3>高级软件工程</h3>
        <p>张教授 · 软件学院</p>
        <div class="course-meta">
          <span>⭐ 4.9 (150评价)</span>
          <span>🕒 36课时</span>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.course-collection h2 {
  font-size: 32px;
  margin-bottom: 25px;
  color: #1a2b50;
}

.course-collection p {
  margin-bottom: 30px;
  color: #4a5568;
  font-size: 20px;
}

.course-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  gap: 25px;
  margin-top: 20px;
}

.course-card {
  background: #f1f7fe;
  border-radius: 12px;
  padding: 25px;
  border-left: 5px solid #3498db;
  transition: transform 0.3s ease;
}

.course-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
}

.course-card h3 {
  font-size: 24px;
  margin-bottom: 10px;
  color: #2c5282;
}

.course-card p {
  margin-bottom: 15px;
  color: #4a5568;
  font-size: 18px;
}

.course-meta {
  display: flex;
  justify-content: space-between;
  color: #4a5568;
  font-size: 16px;
  margin-top: 15px;
}
</style>