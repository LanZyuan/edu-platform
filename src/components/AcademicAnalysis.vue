<template>
  <div class="academic-analysis">
    <h2>学业分析</h2>
    <p>您的学业分析报告：</p>

    <div class="analysis-container">
      <div class="stats-grid">
        <div class="stat-card">
          <div class="stat-value">3.78</div>
          <div class="stat-label">平均绩点</div>
        </div>

        <div class="stat-card">
          <div class="stat-value">92%</div>
          <div class="stat-label">出勤率</div>
        </div>

        <div class="stat-card">
          <div class="stat-value">15</div>
          <div class="stat-label">已完成课程</div>
        </div>

        <div class="stat-card">
          <div class="stat-value">TOP 10%</div>
          <div class="stat-label">专业排名</div>
        </div>
      </div>

      <div class="chart-container">
        <div class="chart-placeholder">
          <h3>学期成绩趋势</h3>
          <p>图表显示区域</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.academic-analysis h2 {
  font-size: 32px;
  margin-bottom: 25px;
  color: #1a2b50;
}

.academic-analysis p {
  margin-bottom: 30px;
  color: #4a5568;
  font-size: 20px;
}

.analysis-container {
  display: grid;
  grid-template-columns: 1fr 2fr;
  gap: 30px;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
}

.stat-card {
  background: #fff;
  border-radius: 12px;
  padding: 25px;
  text-align: center;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.05);
}

.stat-value {
  font-size: 36px;
  font-weight: 700;
  color: #2b6cb0;
  margin-bottom: 10px;
}

.stat-label {
  font-size: 18px;
  color: #4a5568;
}

.chart-container {
  background: #f1f7fe;
  border-radius: 12px;
  padding: 30px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 300px;
}

.chart-placeholder {
  text-align: center;
}

.chart-placeholder h3 {
  font-size: 24px;
  margin-bottom: 15px;
  color: #2c5282;
}

.chart-placeholder p {
  color: #4a5568;
  font-size: 18px;
  margin-bottom: 0;
}
</style>