<template>
  <section id="home" class="banner">
    <div class="container banner-stack">
      <div class="hero">
        <div class="hero-text">
          <p class="eyebrow">SDU NETWORK STUDIO</p>
          <h2>守护校园网络与信息化</h2>
          <div class="hero-tags">
            <span>网络安全小组</span>
            <span>网络运维小组</span>
            <span>新媒体小组</span>
          </div>
          <p class="hero-desc">陪你一起成长</p>
        </div>
        <p class="hero-intro">
          升达网络技术工作室是致力于维护校园网络、为在校师生义务处理电脑故障、宣传推广校内信息化应用的学生组织。
        </p>
        <p class="hero-slogan">
          “服务校园、提升自我”是我们的宗旨。我们为全校师生提供网络技术支持，也是学生实践和竞赛培养的阵地，累计培养数百名技术型人才。
        </p>
      </div>
      <p class="hero-subnote">维护校园网络 · 电脑故障义务处理 · 信息化应用推广</p>
      <div class="group-quick">
        <div class="group-card">
          <h4>网络运维小组</h4>
          <p>保障校园网络畅通，快速响应故障与日常维护。</p>
        </div>
        <div class="group-card">
          <h4>网络安全小组</h4>
          <p>CTF、攻防演练与安全意识建设，筑牢校园安全防线。</p>
        </div>
        <div class="group-card">
          <h4>新媒体小组</h4>
          <p>设计、摄影、视频与公众号运营，点亮校园数字创意。</p>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.banner {
  margin-top: 80px;
  min-height: calc(100vh - 80px);
  position: relative;
  display: flex;
  align-items: center;
  color: var(--color-text);
  overflow: hidden;
}

.banner-stack {
  display: flex;
  flex-direction: column;
  gap: 28px;
  width: 100%;
  align-items: center;
  text-align: center;
}

.hero {
  display: flex;
  flex-direction: column;
  gap: 20px;
  max-width: 840px;
  padding: 16px 0;
}

.hero-text {
  display: flex;
  flex-direction: column;
  gap: 14px;
  align-items: center;
}

.eyebrow {
  font-size: 14px;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--color-muted);
}

.banner h2 {
  font-size: 48px;
  margin-bottom: 20px;
  line-height: 1.15;
  font-family: var(--font-display);
  letter-spacing: 0.5px;
  margin: 0;
}

.hero-tags {
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
  justify-content: center;
}

.hero-tags span {
  padding: 8px 12px;
  border-radius: 999px;
  background: rgba(79, 139, 255, 0.12);
  border: 1px solid rgba(79, 139, 255, 0.3);
  color: var(--color-primary);
  font-size: 14px;
}

.hero-desc {
  font-size: 18px;
  margin: 0;
  line-height: 1.7;
  color: var(--color-text);
}

.hero-slogan {
  margin: 0;
  font-size: 16px;
  line-height: 1.7;
  color: var(--color-muted);
}

.hero-subnote {
  margin: 0;
  font-size: 15px;
  color: var(--color-muted);
  letter-spacing: 0.2px;
}

.banner-btns {
  display: flex;
  gap: 16px;
  flex-wrap: wrap;
  justify-content: center;
}

.banner-btn-secondary {
  background: transparent;
  border: 2px solid rgba(255, 255, 255, 0.7);
  box-shadow: none;
}

.banner-btn-secondary:hover {
  background: rgba(255, 255, 255, 0.14);
  transform: translateY(-4px);
}

.banner-highlights {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  justify-content: center;
}

.banner-highlights span {
  padding: 10px 14px;
  border-radius: 12px;
  background: rgba(79, 139, 255, 0.12);
  border: 1px solid rgba(79, 139, 255, 0.24);
  font-size: 14px;
  color: var(--color-text);
  line-height: 1.2;
}

.group-quick {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 14px;
  width: 100%;
  max-width: 980px;
}

.group-card {
  padding: 16px;
  border-radius: 12px;
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  box-shadow: var(--shadow-card);
}

.group-card h4 {
  margin: 0 0 8px;
  font-size: 16px;
  color: var(--color-text);
}

.group-card p {
  margin: 0;
  font-size: 14px;
  line-height: 1.6;
  color: var(--color-muted);
}

.cta-note {
  margin: 2px 0 0;
  font-size: 14px;
  color: var(--color-muted);
  letter-spacing: 0.1px;
  text-align: center;
}

@media (max-width: 992px) {
  .banner {
    height: auto;
    padding: 120px 0 80px;
  }

  .banner h2 {
    font-size: 36px;
  }

  .hero-desc {
    font-size: 16px;
  }

  .banner-btns {
    gap: 12px;
  }

  .banner-highlights span {
    font-size: 13px;
  }

  .group-card {
    padding: 14px;
  }
}
</style>
