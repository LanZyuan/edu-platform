<template>
  <div class="wrong-question-book">
    <h2>错题本</h2>
    <p>您的错题记录：</p>

    <div class="question-list">
      <div class="question-item">
        <div class="question-header">
          <span class="subject-tag">线性代数</span>
          <span class="date">2023-10-15</span>
        </div>
        <div class="question-content">
          <p>矩阵A=[1,2;3,4]，求A的逆矩阵。</p>
        </div>
        <div class="question-actions">
          <button class="review-btn">复习</button>
          <button class="delete-btn">删除</button>
        </div>
      </div>

      <div class="question-item">
        <div class="question-header">
          <span class="subject-tag">概率统计</span>
          <span class="date">2023-10-10</span>
        </div>
        <div class="question-content">
          <p>贝叶斯定理的应用：已知P(A)=0.3, P(B|A)=0.8, P(B|A')=0.4，求P(A|B)。</p>
        </div>
        <div class="question-actions">
          <button class="review-btn">复习</button>
          <button class="delete-btn">删除</button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.wrong-question-book h2 {
  font-size: 32px;
  margin-bottom: 25px;
  color: #1a2b50;
}

.wrong-question-book p {
  margin-bottom: 30px;
  color: #4a5568;
  font-size: 20px;
}

.question-list {
  display: grid;
  gap: 20px;
}

.question-item {
  background: #fff;
  border-radius: 12px;
  padding: 25px;
  border: 1px solid #e2e8f0;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
}

.question-header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 15px;
  padding-bottom: 10px;
  border-bottom: 1px solid #f0f4f8;
}

.subject-tag {
  background: #ffebee;
  color: #c62828;
  padding: 5px 12px;
  border-radius: 20px;
  font-size: 16px;
  font-weight: 500;
}

.date {
  color: #718096;
  font-size: 16px;
}

.question-content p {
  margin-bottom: 0;
  font-size: 18px;
  line-height: 1.6;
}

.question-actions {
  display: flex;
  gap: 15px;
  margin-top: 20px;
}

.review-btn, .delete-btn {
  padding: 10px 20px;
  border-radius: 6px;
  font-size: 16px;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.3s;
}

.review-btn {
  background: #e3f2fd;
  color: #1565c0;
  border: none;
}

.review-btn:hover {
  background: #bbdefb;
}

.delete-btn {
  background: #ffebee;
  color: #c62828;
  border: none;
}

.delete-btn:hover {
  background: #ffcdd2;
}
</style>