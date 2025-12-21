<template>
  <section id="network" class="contact">
    <div class="container">
      <div class="section-title">
        <h2>校园网服务</h2>
        <p>报修、反馈与咨询渠道，保障你的网络与设备畅通。</p>
      </div>
      <div class="contact-content">
        <div class="contact-info">
          <h3>快速报修</h3>
          <div class="contact-item" v-for="info in contactInfos" :key="info.title">
            <div class="contact-icon">
              <i :class="info.icon"></i>
            </div>
            <div class="contact-text">
              <h4>{{ info.title }}</h4>
              <p>{{ info.desc }}</p>
            </div>
          </div>
          <div class="contact-qrcode">
            <h4>公众号报修/资讯</h4>
            <div class="qrcode-img">
              <img src="https://placehold.co/150x150/ffffff/165dff?text=QR" alt="升达网络技术工作室公众号" />
            </div>
            <p class="qrcode-tips">扫码关注，提交报修或查看使用指南</p>
          </div>
        </div>
        <div class="contact-map">
          <h3>问题反馈</h3>
          <p>填写你的网络/设备问题或建议，我们会尽快跟进。</p>
          <form @submit.prevent="submitFeedback">
            <div class="form-group">
              <label for="issueType">问题类型</label>
              <select id="issueType" class="form-control" v-model="feedback.issueType">
                <option>宿舍网络</option>
                <option>校园WiFi</option>
                <option>账号/认证</option>
                <option>打印设备</option>
                <option>其他</option>
              </select>
            </div>
            <div class="form-group">
              <label for="issueDesc">问题描述</label>
              <textarea
                id="issueDesc"
                class="form-control"
                v-model="feedback.issueDesc"
                placeholder="请描述问题现象、宿舍楼栋/房间、时间等信息"
              ></textarea>
            </div>
            <div class="form-group">
              <label for="contactInfo">联系方式</label>
              <input
                id="contactInfo"
                class="form-control"
                v-model="feedback.contactInfo"
                placeholder="手机或QQ，便于联系"
              />
            </div>
            <button type="submit" class="btn full-btn">提交反馈</button>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { reactive } from 'vue'

const contactInfos = [
  { icon: 'fas fa-phone', title: '联系电话', desc: '校园网报修电话：0371-85911009' },
  { icon: 'fas fa-comments', title: 'QQ群咨询', desc: '网络资讯群：256244365' },
  { icon: 'fas fa-wifi', title: '线上报修', desc: '关注“升达网络技术工作室”公众号，进入报修入口。' },
]

const feedback = reactive({
  issueType: '宿舍网络',
  issueDesc: '',
  contactInfo: '',
})

const submitFeedback = () => {
  alert('反馈已提交，我们将尽快跟进！')
  feedback.issueType = '宿舍网络'
  feedback.issueDesc = ''
  feedback.contactInfo = ''
}
</script>

<style scoped>
.contact {
  background: linear-gradient(180deg, rgba(255, 255, 255, 0.95) 0%, rgba(241, 240, 255, 0.78) 100%);
  position: relative;
}

.contact::before {
  content: '';
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 18% 12%, rgba(255, 111, 97, 0.16), transparent 32%),
    radial-gradient(circle at 78% 8%, rgba(124, 58, 237, 0.16), transparent 32%);
  pointer-events: none;
}

.contact-content {
  display: flex;
  flex-wrap: wrap;
  gap: 50px;
  position: relative;
  z-index: 1;
}

.contact-info {
  flex: 1;
  min-width: 300px;
}

.contact-info h3 {
  font-size: 24px;
  margin-bottom: 30px;
  color: var(--color-text);
  font-weight: 700;
}

.contact-item {
  display: flex;
  align-items: flex-start;
  margin-bottom: 20px;
}

.contact-icon {
  width: 40px;
  height: 40px;
  background: rgba(124, 58, 237, 0.12);
  color: var(--color-secondary);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: 15px;
  flex-shrink: 0;
  box-shadow: 0 10px 25px rgba(124, 58, 237, 0.16);
}

.contact-text h4 {
  font-size: 16px;
  margin-bottom: 5px;
  color: var(--color-text);
  font-weight: 700;
}

.contact-text p {
  font-size: 14px;
  color: var(--color-muted);
  line-height: 1.6;
}

.contact-qrcode {
  margin-top: 30px;
}

.contact-qrcode h4 {
  font-size: 16px;
  margin-bottom: 15px;
  color: var(--color-text);
}

.qrcode-img {
  width: 150px;
  height: 150px;
  border: 1px solid rgba(255, 255, 255, 0.6);
  padding: 10px;
  border-radius: var(--radius-md);
  box-shadow: var(--shadow-card);
  background: rgba(255, 255, 255, 0.9);
}

.qrcode-img img {
  width: 100%;
  height: 100%;
  object-fit: contain;
}

.qrcode-tips {
  margin-top: 10px;
  font-size: 14px;
  color: var(--color-muted);
}

.contact-map {
  flex: 2;
  min-width: 300px;
  height: auto;
  background: linear-gradient(150deg, rgba(255, 255, 255, 0.92), rgba(245, 233, 255, 0.82));
  padding: 24px;
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-card);
  border: 1px solid rgba(255, 255, 255, 0.5);
}

.contact-map h3 {
  color: var(--color-text);
  font-weight: 700;
  margin-bottom: 15px;
}

.contact-map p {
  color: var(--color-muted);
  margin-bottom: 15px;
}

.full-btn {
  width: 100%;
}
</style>
