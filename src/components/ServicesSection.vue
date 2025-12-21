<template>
  <section id="services" class="services">
    <div class="container">
      <div class="section-title">
        <h2>服务中心</h2>
        <p>内修、外修、星印云自助打印机维修三大业务，覆盖校园网与设备全场景。</p>
      </div>
      <div class="services-list">
        <div class="service-card" v-for="service in services" :key="service.title">
          <div class="service-icon">
            <i :class="service.icon"></i>
          </div>
          <h3>{{ service.title }}</h3>
          <p>{{ service.desc }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
const services = [
  { icon: 'fas fa-wifi', title: '内修服务', desc: '校园网账号问题、IP绑定、宿舍网络故障排查与修复，保障校内网络畅通。' },
  { icon: 'fas fa-laptop-code', title: '外修服务', desc: '电脑系统安装、软件指导、网线制作、网络安全咨询，面向师生的上门/预约支持。' },
  { icon: 'fas fa-project-diagram', title: '星印云打印机', desc: '星印云自助打印机维护、故障处理与耗材支持，让打印更稳定、更省心。' },
]
</script>

<style scoped>
.services-list {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 30px;
}

.service-card {
  background: linear-gradient(145deg, rgba(255, 255, 255, 0.78), rgba(255, 255, 255, 0.68));
  padding: 30px;
  border-radius: var(--radius-lg);
  text-align: center;
  transition: all 0.35s ease;
  box-shadow: var(--shadow-card);
  border: 1px solid rgba(255, 255, 255, 0.35);
}

.service-card:hover {
  transform: translateY(-8px) scale(1.01);
  box-shadow: var(--shadow-soft);
}

.service-icon {
  font-size: 48px;
  color: var(--color-secondary);
  margin-bottom: 20px;
  text-shadow: 0 10px 30px rgba(124, 58, 237, 0.25);
}

.service-card h3 {
  font-size: 20px;
  margin-bottom: 15px;
  color: var(--color-text);
  font-weight: 700;
}

.service-card p {
  font-size: 14px;
  color: var(--color-muted);
  line-height: 1.7;
}

@media (max-width: 768px) {
  .services-list {
    grid-template-columns: 1fr;
  }
}
</style>
