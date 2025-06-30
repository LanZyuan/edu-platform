<template>
  <div class="study-progress">
    <h2>个人修读情况</h2>
    <p>您的课程学习进度：</p>

    <div class="progress-container">
      <div class="progress-item">
        <div class="progress-header">
          <h3>数据结构与算法</h3>
          <span>85%</span>
        </div>
        <div class="progress-bar">
          <div class="progress-fill" style="width: 85%"></div>
        </div>
      </div>

      <div class="progress-item">
        <div class="progress-header">
          <h3>计算机网络原理</h3>
          <span>70%</span>
        </div>
        <div class="progress-bar">
          <div class="progress-fill" style="width: 70%"></div>
        </div>
      </div>

      <div class="progress-item">
        <div class="progress-header">
          <h3>高级软件工程</h3>
          <span>60%</span>
        </div>
        <div class="progress-bar">
          <div class="progress-fill" style="width: 60%"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.study-progress h2 {
  font-size: 32px;
  margin-bottom: 25px;
  color: #1a2b50;
}

.study-progress p {
  margin-bottom: 30px;
  color: #4a5568;
  font-size: 20px;
}

.progress-container {
  display: grid;
  gap: 30px;
  max-width: 800px;
  margin-top: 20px;
}

.progress-item {
  background: #fff;
  border-radius: 12px;
  padding: 25px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.05);
}

.progress-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 15px;
}

.progress-header h3 {
  font-size: 22px;
  color: #2d3748;
}

.progress-header span {
  font-size: 24px;
  font-weight: 600;
  color: #2b6cb0;
}

.progress-bar {
  height: 20px;
  background: #e2e8f0;
  border-radius: 10px;
  overflow: hidden;
}

.progress-fill {
  height: 100%;
  background: linear-gradient(90deg, #3498db, #2b6cb0);
  border-radius: 10px;
}
</style>