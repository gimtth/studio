<template>
  <footer class="footer">
    <div class="container">
      <div class="footer-content">
        <div class="footer-logo">
          <img src="/logo.png" alt="升达网络技术工作室Logo" />
          <p>技术服务校园，实践成就成长。郑州升达经贸管理学院学生技术组织，致力于校园信息化建设与技术人才培养。</p>
        </div>
        <div class="footer-links">
          <h4>快速导航</h4>
          <ul>
            <li><a href="#home">首页</a></li>
            <li><a href="#about">关于我们</a></li>
            <li><a href="#services">服务中心</a></li>
            <li><a href="#activities">活动动态</a></li>
            <li><a href="#recruitment">招新专栏</a></li>
          </ul>
        </div>
        <div class="footer-links">
          <h4>相关链接</h4>
          <ul>
            <li><a href="https://www.shengda.edu.cn/" target="_blank">郑州升达经贸管理学院官网</a></li>
            <li><a href="https://xxhc.shengda.edu.cn/" target="_blank">郑州升达经贸管理学院信息化处</a></li>
            <li><a href="https://cas.shengda.edu.cn/" target="_blank">智慧校园</a></li>
          </ul>
        </div>
      </div>
      <div class="footer-bottom">
        <p>© 2025 升达网络技术工作室 版权所有 | 地址：郑州升达经贸管理学院资讯楼319室</p>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  background: linear-gradient(135deg, rgba(63, 76, 146, 0.9), rgba(104, 83, 220, 0.85));
  color: #fff;
  padding: 50px 0 20px;
  position: relative;
  overflow: hidden;
  isolation: isolate;
}

.footer-content {
  display: flex;
  flex-wrap: wrap;
  gap: 50px;
  margin-bottom: 30px;
}

.footer-logo {
  flex: 1;
  min-width: 300px;
}

.footer-logo img {
  height: 60px;
  margin-bottom: 15px;
  filter: drop-shadow(0 10px 25px rgba(0, 0, 0, 0.2));
}

.footer-logo p {
  font-size: 14px;
  color: rgba(255, 255, 255, 0.8);
  line-height: 1.6;
  max-width: 300px;
}

.footer-links {
  flex: 1;
  min-width: 200px;
}

.footer-links h4 {
  font-size: 18px;
  margin-bottom: 20px;
  position: relative;
  padding-bottom: 10px;
  letter-spacing: 0.4px;
}

.footer-links h4::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 40px;
  height: 2px;
  background: linear-gradient(90deg, rgba(255, 111, 97, 0.85), rgba(246, 195, 68, 0.85));
}

.footer-links ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.footer-links li {
  margin-bottom: 10px;
}

.footer-links a {
  color: rgba(255, 255, 255, 0.8);
  font-size: 14px;
  transition: color 0.3s;
}

.footer-links a:hover {
  color: #fff;
}

.footer-bottom {
  text-align: center;
  padding-top: 20px;
  border-top: 1px solid rgba(255, 255, 255, 0.2);
  font-size: 12px;
  color: rgba(255, 255, 255, 0.6);
}
</style>
