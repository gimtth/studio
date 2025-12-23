<template>
  <section id="activities" class="activities">
    <div class="container">
      <div class="section-title">
        <h2>活动动态</h2>
        <p>记录我们的技术成长与精彩瞬间，包含技术培训、竞赛参与、校园活动等</p>
      </div>
      <div class="activity-filters">
        <div
          v-for="btn in filters"
          :key="btn"
          class="filter-btn"
          :class="{ active: activeFilter === btn }"
          @click="activeFilter = btn"
        >
          {{ btn }}
        </div>
      </div>
      <div class="activities-list">
        <div
          class="activity-card"
          v-for="card in filteredCards"
          :key="card.title"
        >
          <div class="activity-img">
            <img :src="card.img" :alt="card.title" />
          </div>
          <div class="activity-info">
            <span class="activity-date">{{ card.date }}</span>
            <h3>{{ card.title }}</h3>
            <p>{{ card.desc }}</p>
            <a href="#" class="btn">查看详情</a>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue'

type Card = {
  title: string
  desc: string
  date: string
  img: string
  category: string
}

const filters = ['全部活动', '技术培训', '竞赛参与', '校园活动']
const activeFilter = ref<string>('全部活动')

const cards: Card[] = [
  {
    title: '第十四届“新华三杯”全国技术大赛获佳绩',
    desc: '工作室团队代表学校参加全国总决赛，凭借扎实的网络技术功底和协作能力，荣获全国团队二等奖，为校争光！',
    date: '2025-05-18',
    img: '/h1.jpg',
    category: '竞赛参与',
  },
  {
    title: '新生培训活动',
    desc: '面向新生开展基础网络配置、账号安全与常用软件培训，帮助大家快速适应校园数字生活。',
    date: '2025-09-05',
    img: '/h3.jpg',
    category: '技术培训',
  },
  {
    title: '运动会',
    desc: '工作室自办趣味运动会，策划接力、拔河等项目，组织报名与裁判，保障场地秩序与后勤，让成员在竞技中团结互动。',
    date: '2025-09-10',
    img: '/h2.JPG',
    category: '校园活动',
  },
]

const filteredCards = computed(() =>
  activeFilter.value === '全部活动'
    ? cards
    : cards.filter((c) => c.category === activeFilter.value)
)
</script>

<style scoped>
.activities {
  background: linear-gradient(180deg, rgba(255, 255, 255, 0.92) 0%, rgba(245, 233, 255, 0.75) 100%);
  position: relative;
  overflow: hidden;
}

.activities::before {
  content: '';
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 12% 18%, rgba(255, 111, 97, 0.16), transparent 35%),
    radial-gradient(circle at 82% 12%, rgba(124, 58, 237, 0.16), transparent 30%);
  pointer-events: none;
}

.activity-filters {
  text-align: center;
  margin-bottom: 40px;
}

.filter-btn {
  display: inline-block;
  padding: 10px 18px;
  margin: 0 8px 10px;
  background: rgba(255, 255, 255, 0.82);
  border-radius: 20px;
  font-size: 14px;
  cursor: pointer;
  transition: all 0.3s;
  border: 1px solid rgba(255, 255, 255, 0.6);
  box-shadow: 0 8px 25px rgba(20, 10, 60, 0.08);
}

.filter-btn.active {
  background: linear-gradient(135deg, var(--color-primary), var(--color-secondary));
  color: #fff;
  box-shadow: var(--shadow-card);
}

.activities-list {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 30px;
}

.activity-card {
  background: linear-gradient(155deg, rgba(255, 255, 255, 0.9), rgba(255, 255, 255, 0.75));
  border-radius: var(--radius-lg);
  overflow: hidden;
  box-shadow: var(--shadow-card);
  transition: all 0.35s ease;
  border: 1px solid rgba(255, 255, 255, 0.5);
  display: flex;
  flex-direction: column;
  height: 100%;
}

.activity-card:hover {
  transform: translateY(-6px) scale(1.01);
  box-shadow: var(--shadow-soft);
}

.activity-img {
  height: 200px;
  overflow: hidden;
}

.activity-img img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s;
}

.activity-card:hover .activity-img img {
  transform: scale(1.05);
}

.activity-info {
  padding: 20px;
  display: flex;
  flex-direction: column;
  flex: 1;
}

.activity-date {
  font-size: 12px;
  color: var(--color-muted);
  margin-bottom: 10px;
  display: block;
}

.activity-card h3 {
  font-size: 18px;
  margin-bottom: 10px;
  color: var(--color-text);
  font-weight: 700;
}

.activity-card p {
  font-size: 14px;
  color: var(--color-muted);
  margin-bottom: 15px;
  line-height: 1.7;
}

.activity-card .btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-height: 40px;
  padding: 0 16px;
  margin-top: auto;
}

@media (max-width: 992px) {
  .activities-list {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 768px) {
  .activities-list {
    grid-template-columns: 1fr;
  }
}
</style>
