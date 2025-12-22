<template>
  <section id="recruitment" class="recruitment">
    <div class="container">
      <div class="section-title">
        <h2>招新专栏</h2>
        <p>当前招新暂未开放，敬请关注公众号或QQ群通知。</p>
      </div>
      <div class="recruitment-content">
        <div class="recruitment-text">
          <h3>招新暂未开放</h3>
          <p>感谢关注！本期招新通道尚未开启，请持续留意“升达网络技术工作室”公众号或QQ群公告，开放时间与流程将第一时间发布。</p>
          <div class="recruitment-requirements">
            <h4>敬请关注</h4>
            <p class="muted">招新开放后将公布具体时间、流程与要求，敬请耐心等待。</p>
          </div>
          <h4>报名通道</h4>
          <p class="muted">目前在线报名与纸质报名均未开放，开启后将在此处更新入口。</p>
        </div>
        <div class="recruitment-form">
          <h3 class="form-title">在线报名</h3>
          <div class="form-closed">暂未开放，敬请期待</div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts"></script>

<style scoped>
.recruitment {
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.9), rgba(241, 240, 255, 0.82));
  position: relative;
  overflow: hidden;
}

.recruitment::before {
  content: '';
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 18% 18%, rgba(255, 111, 97, 0.16), transparent 32%),
    radial-gradient(circle at 82% 12%, rgba(124, 58, 237, 0.16), transparent 30%);
  pointer-events: none;
}

.recruitment-content {
  position: relative;
  z-index: 1;
  display: flex;
  flex-wrap: wrap;
  gap: 50px;
  align-items: center;
}

.recruitment-text {
  flex: 1;
  min-width: 300px;
}

.recruitment-text h3 {
  font-size: 28px;
  color: var(--color-primary);
  margin-bottom: 20px;
  font-family: var(--font-display);
}

.recruitment-text p {
  font-size: 16px;
  color: var(--color-muted);
  margin-bottom: 20px;
  line-height: 1.8;
}

.recruitment-requirements h4 {
  font-size: 20px;
  margin-bottom: 15px;
  color: var(--color-secondary);
  letter-spacing: 0.3px;
}

.requirements-list {
  list-style: none;
  margin-bottom: 30px;
}

.requirements-list li {
  font-size: 16px;
  color: var(--color-text);
  margin-bottom: 10px;
  display: flex;
  align-items: center;
}

.requirements-list li::before {
  content: '✓';
  color: var(--color-primary);
  margin-right: 10px;
  font-weight: bold;
}

.recruitment-form {
  flex: 1;
  min-width: 300px;
  background: linear-gradient(150deg, rgba(255, 255, 255, 0.9), rgba(245, 233, 255, 0.82));
  padding: 30px;
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-card);
  border: 1px solid rgba(255, 255, 255, 0.6);
}

.form-title {
  text-align: center;
  margin-bottom: 20px;
  color: var(--color-secondary);
  font-family: var(--font-display);
}

.form-closed {
  text-align: center;
  padding: 28px;
  border: 1px dashed rgba(0, 0, 0, 0.1);
  border-radius: var(--radius-md);
  background: rgba(255, 255, 255, 0.85);
  color: var(--color-muted);
  font-weight: 600;
}

.muted {
  color: var(--color-muted);
}
</style>
