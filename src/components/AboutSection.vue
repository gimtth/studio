<template>
  <section id="about" class="about">
    <div class="container">
      <div class="section-title">
        <h2>兴趣小组</h2>
        <p>网络安全、网络运维、新媒体三大兴趣小组，技术讨论、攻防演练、创意设计齐头并进。</p>
      </div>
      <div class="about-content solo">
        <div class="org-structure">
          <h4>兴趣小组</h4>
          <div class="org-list">
            <button
              v-for="item in groups"
              :key="item.id"
              class="org-item"
              :class="{ active: selectedId === item.id }"
              @click="selectGroup(item.id)"
            >
              <h5>{{ item.title }}</h5>
              <p>{{ item.desc }}</p>
            </button>
          </div>
        </div>

        <div class="group-detail" v-if="currentGroup && currentGroup.id === 'security' && currentSlide">
          <div class="group-detail-text">
            <div class="text-block">
              <p class="group-tag">{{ currentGroup.title }}</p>
              <p class="group-desc emphasis">{{ currentGroup.detail }}</p>
            </div>
            <div class="image-block">
              <div class="image-wrapper" @click="openZoom">
                <img :src="currentSlide.img" :alt="currentGroup.title" />
              </div>
              <div class="group-actions">
                <button class="ghost-btn" @click="prevSlide">‹</button>
                <span class="indicator">{{ slideIndex + 1 }} / {{ displayCount }}</span>
                <button class="ghost-btn" @click="nextSlide">›</button>
              </div>
            </div>
          </div>
        </div>

        <div v-if="isZoomOpen && currentSlide" class="zoom-overlay" @click.self="closeZoom">
          <div class="zoom-content">
            <button class="close-btn" @click="closeZoom">×</button>
            <img :src="currentSlide.img" :alt="currentGroup?.title" />
          </div>
        </div>

      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { computed, ref, watch } from 'vue'

const groups = [
  {
    id: 'security',
    title: '网络安全小组',
    desc: 'CTF、攻防演练、渗透测试、安全意识提升',
    detail:
      '2025年第十四届“新华三杯”全国大学生数字技术省复赛圆满结束，升达网络技术工作室共有32名参赛成员，27名进入复赛，经过激烈角逐，最终12人脱颖而出，斩获佳绩！',
    slides: [
      {
        img: '/w1.jpg',
      },
      {
        img: '/w2.jpg',
      },
    ],
  },
  {
    id: 'network',
    title: '网络运维小组',
    desc: '校园网络维护与优化、应急保障、技术讨论',
    detail: '（敬请期待更多活动内容）',
    slides: [],
  },
  {
    id: 'media',
    title: '新媒体小组',
    desc: '平面设计、摄影视频、公众号运营与活动宣传',
    detail: '（敬请期待更多活动内容）',
    slides: [],
  },
]

const selectedId = ref(groups[0]?.id ?? '')
const slideIndex = ref(0)
const isZoomOpen = ref(false)

const currentGroup = computed(() => groups.find((g) => g.id === selectedId.value) ?? groups[0])
const slideCount = computed(() => currentGroup.value?.slides.length ?? 0)
const currentSlide = computed(() => currentGroup.value?.slides[slideIndex.value] ?? currentGroup.value?.slides[0] ?? null)
const displayCount = computed(() => (slideCount.value ? slideCount.value : 1))

const selectGroup = (id: string) => {
  selectedId.value = id
  slideIndex.value = 0
}

const nextSlide = () => {
  if (!currentGroup.value || slideCount.value < 2) return
  slideIndex.value = (slideIndex.value + 1) % currentGroup.value.slides.length
}

const prevSlide = () => {
  if (!currentGroup.value || slideCount.value < 2) return
  slideIndex.value = (slideIndex.value + currentGroup.value.slides.length - 1) % currentGroup.value.slides.length
}

const openZoom = () => {
  if (!currentSlide.value) return
  isZoomOpen.value = true
}

const closeZoom = () => {
  isZoomOpen.value = false
}

watch([selectedId, slideIndex], () => {
  isZoomOpen.value = false
})

</script>

<style scoped>
.about {
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.9) 0%, rgba(246, 233, 255, 0.75) 100%);
}

.about-content {
  display: flex;
  flex-wrap: wrap;
  align-items: flex-start;
  gap: 32px;
}

.org-structure {
  margin-top: 30px;
  width: 100%;
}

.org-structure h4 {
  font-size: 20px;
  margin-bottom: 15px;
  color: var(--color-secondary);
  letter-spacing: 0.5px;
}

.org-list {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 20px;
  width: 100%;
  justify-items: stretch;
}

.org-item {
  background: linear-gradient(145deg, rgba(255, 255, 255, 0.9), rgba(255, 255, 255, 0.7));
  padding: 18px 22px;
  border-radius: var(--radius-md);
  box-shadow: var(--shadow-card);
  text-align: center;
  border: 1px solid rgba(255, 255, 255, 0.5);
  position: relative;
  transition: transform 0.2s ease, box-shadow 0.2s ease, border-color 0.2s ease;
}

.org-item.active {
  border-color: rgba(79, 139, 255, 0.8);
  background: rgba(79, 139, 255, 0.12);
  box-shadow: 0 12px 32px rgba(79, 139, 255, 0.2);
}

.org-item::after {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: var(--radius-md);
  border: 2px solid transparent;
  transition: border-color 0.2s ease;
}

.org-item:hover {
  transform: translateY(-6px) scale(1.01);
  box-shadow: 0 14px 36px rgba(79, 139, 255, 0.18);
}

.org-item:hover::after {
  border-color: rgba(79, 139, 255, 0.35);
}

.org-item h5 {
  font-size: 16px;
  color: var(--color-text);
  margin-bottom: 6px;
  font-weight: 700;
}

.org-item p {
  font-size: 14px;
  color: var(--color-muted);
  margin-bottom: 0;
  line-height: 1.6;
}

.group-detail {
  width: 100%;
  background: rgba(255, 255, 255, 0.9);
  border: 1px solid rgba(255, 255, 255, 0.6);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-card);
  padding: 22px;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
  position: relative;
}

.group-detail:hover {
  transform: translateY(-6px);
  box-shadow: 0 14px 38px rgba(79, 139, 255, 0.2);
}

.group-detail::after {
  content: '';
  position: absolute;
  inset: 12px;
  border-radius: var(--radius-md);
  border: 1px solid rgba(79, 139, 255, 0.15);
  pointer-events: none;
  opacity: 0;
  transition: opacity 0.2s ease;
}

.group-detail:hover::after {
  opacity: 1;
}

.group-detail-text {
  display: flex;
  align-items: flex-start;
  gap: 18px;
}

.text-block {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.group-tag {
  margin: 0;
  font-size: 14px;
  color: var(--color-primary);
  font-weight: 600;
  letter-spacing: 0.3px;
}

.group-desc {
  margin: 0;
  font-size: 15px;
  line-height: 1.7;
  color: var(--color-muted);
}

.group-actions {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-top: 10px;
  justify-content: center;
}

.ghost-btn {
  background: rgba(79, 139, 255, 0.12);
  color: var(--color-primary);
  border: 1px solid rgba(79, 139, 255, 0.3);
  border-radius: 8px;
  padding: 6px 10px;
  cursor: pointer;
  transition: all 0.2s ease;
}

.ghost-btn:hover {
  background: rgba(79, 139, 255, 0.2);
}

.indicator {
  font-size: 14px;
  color: var(--color-muted);
}

.image-block {
  flex: 0 0 36%;
  max-width: 360px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.image-wrapper {
  width: 100%;
  position: relative;
  cursor: zoom-in;
}

.image-block img {
  width: 100%;
  aspect-ratio: 16 / 9;
  height: auto;
  border-radius: var(--radius-md);
  box-shadow: var(--shadow-card);
  object-fit: cover;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.image-wrapper:hover img {
  transform: scale(1.02);
  box-shadow: 0 16px 36px rgba(0, 0, 0, 0.2);
}

.zoom-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.65);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 16px;
  z-index: 999;
}

.zoom-content {
  position: relative;
  max-width: min(900px, 90vw);
  max-height: 85vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.zoom-content img {
  width: 100%;
  height: 100%;
  object-fit: contain;
  border-radius: var(--radius-md);
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.35);
  background: #fff;
}

.close-btn {
  position: absolute;
  top: -10px;
  right: -10px;
  background: #fff;
  border: none;
  width: 32px;
  height: 32px;
  border-radius: 50%;
  font-size: 18px;
  cursor: pointer;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.25);
  color: #333;
}

.close-btn:hover {
  background: #f2f2f2;
}

@media (max-width: 768px) {
  .group-detail-text {
    flex-direction: column;
  }

  .group-detail-text.reverse {
    flex-direction: column;
  }

  .image-block {
    width: 100%;
    max-width: 100%;
  }
}
</style>
