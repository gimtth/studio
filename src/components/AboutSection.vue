<template>
  <section id="about" class="about">
    <div class="container">
      <div class="section-title">
        <h2>兴趣小组</h2>
        <p>网络安全、网络运维、新媒体三大兴趣小组，技术讨论、攻防演练、创意设计齐头并进。</p>
      </div>
      <div class="about-content solo">
        <div class="org-structure">
          <div class="group-intro">
            <div class="intro-item">
              <h5 class="intro-title">网络运维小组</h5>
              <p>
              网络运维是校园信息流动的命脉，而运维工程师则是这命脉的守护者。我们专注于校园网络基础设施的维护与优化，定期召开技术讨论会，直击网络管理的核心挑战。无论是日常的网络维护工作，还是突发的网络故障，我们都能迅速响应、高效处置，全力保障校园网络的畅通无阻。
              </p>
            </div>
            <div class="intro-item">
              <h5 class="intro-title">网络安全小组</h5>
              <p>
              网络安全不仅是守护我们信息安全的前沿阵地，更是一个专注于提升网络安全意识与技能的交流平台。我们的兴趣小组以CTF竞赛、攻防对抗演练、渗透测试等多元形式为载体，深入开展技术研讨与实践探索。在这里，我们共同分享技术心得，在交流碰撞中持续精进能力，共同筑牢网络安全的防线。
              </p>
            </div>
            <div class="intro-item">
              <h5 class="intro-title">新媒体小组</h5>
              <p>
              新媒体是创意与传播的桥梁。从平面设计的斑斓色彩到视频编辑的时光魔法，我们把握PS、摄影与视频制作的精髓，更通过运营微信公众号引领着校园文化的潮流动向。每周的技能培训与创意头脑风暴，总能点燃你的视觉想象，让灵感在指尖流转，最终落地成让人眼前一亮的数字作品。
              </p>
            </div>
          </div>
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
                <div class="image-nav" @click.stop>
                  <button class="nav-btn" @click.stop="prevSlide">‹</button>
                  <button class="nav-btn" @click.stop="nextSlide">›</button>
                  <span class="image-indicator">{{ slideIndex + 1 }} / {{ displayCount }}</span>
                </div>
              </div>
            </div>
          </div>
        </div>

        

        <div class="group-detail" v-if="currentGroup && currentGroup.id === 'security'">
          <div class="group-detail-text">
            <div class="image-block">
              <div class="image-wrapper">
                <img src="/w3.jpg" alt="新华三杯省赛精彩瞬间" />
              </div>
            </div>
            <div class="text-block">
              <p class="group-tag">网络安全小组</p>
              <p class="group-desc emphasis">
                热烈祝贺2025年“新华三杯”全国大学生数字技术省级赛圆满结束，本次大赛由全省38所高校的814名选手参赛。其中升达网络技术工作室共有15名参赛人员，经过激烈比拼，一路闯关。最终，9名同学脱颖而出，斩获亮眼佳绩。
              </p>
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
    desc: '网络运维是校园信息流动的命脉，而运维工程师则是这命脉的守护者。我们专注于校园网络基础设施的维护与优化，定期召开技术讨论会，直击网络管理的核心挑战。无论是日常的网络维护工作，还是突发的网络故障，我们都能迅速响应、高效处置，全力保障校园网络的畅通无阻。',
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
    desc: '网络安全不仅是守护我们信息安全的前沿阵地，更是一个专注于提升网络安全意识与技能的交流平台。我们的兴趣小组以CTF竞赛、攻防对抗演练、渗透测试等多元形式为载体，深入开展技术研讨与实践探索。在这里，我们共同分享技术心得，在交流碰撞中持续精进能力，共同筑牢网络安全的防线。',
    detail: '（敬请期待更多活动内容）',
    slides: [],
  },
  {
    id: 'media',
    title: '新媒体小组',
    desc: '新媒体是创意与传播的桥梁。从平面设计的斑斓色彩到视频编辑的时光魔法，我们把握PS、摄影与视频制作的精髓，更通过运营微信公众号引领着校园文化的潮流动向。每周的技能培训与创意头脑风暴，总能点燃你的视觉想象，让灵感在指尖流转，最终落地成让人眼前一亮的数字作品。',
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

.about .section-title {
  margin-bottom: 16px;
  padding-top: 8px;
}

.group-intro {
  margin-bottom: 14px;
  display: grid;
  gap: 12px;
}

.intro-item {
  background: rgba(255, 255, 255, 0.72);
  border: 1px solid rgba(79, 139, 255, 0.12);
  border-radius: var(--radius-md);
  padding: 12px 14px;
  box-shadow: 0 6px 22px rgba(0, 0, 0, 0.05);
  position: relative;
  overflow: hidden;
  transition: transform 0.2s ease, box-shadow 0.2s ease, border-color 0.2s ease;
}

.intro-title {
  margin: 0 0 6px;
  font-size: 16px;
  font-weight: 800;
  letter-spacing: 0.6px;
  background: linear-gradient(120deg, #4f8bff, #7c5bff 60%, #ff7ad6);
  background-clip: text;
  -webkit-background-clip: text;
  color: transparent;
  display: inline-flex;
  align-items: center;
  gap: 8px;
  position: relative;
  padding-right: 6px;
  transition: transform 0.2s ease, opacity 0.2s ease;
}

.intro-title::after {
  content: '';
  position: absolute;
  left: 0;
  bottom: -3px;
  width: 100%;
  height: 2px;
  background: linear-gradient(120deg, #4f8bff, #ff7ad6);
  transform: scaleX(0);
  transform-origin: left;
  transition: transform 0.25s ease;
}

.intro-item:hover .intro-title {
  transform: translateY(-1px);
}

.intro-item:hover .intro-title::after {
  transform: scaleX(1);
}

.intro-item::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(120deg, rgba(79, 139, 255, 0.12), rgba(255, 122, 214, 0.12));
  opacity: 0;
  transition: opacity 0.2s ease;
}

.intro-item:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 28px rgba(0, 0, 0, 0.08);
  border-color: rgba(79, 139, 255, 0.35);
}

.intro-item:hover::before {
  opacity: 1;
}

.intro-item p {
  margin: 0;
  line-height: 1.65;
  color: var(--color-muted);
  text-indent: 2em;
}

.about-content {
  display: flex;
  flex-wrap: wrap;
  align-items: flex-start;
  gap: 32px;
}

.org-structure {
  margin-top: 12px;
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
  grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
  gap: 10px;
  width: 100%;
  justify-items: center;
  align-items: stretch;
}

.org-item {
  background: linear-gradient(145deg, rgba(255, 255, 255, 0.9), rgba(255, 255, 255, 0.7));
  padding: 14px 16px 12px;
  border-radius: var(--radius-md);
  box-shadow: var(--shadow-card);
  text-align: center;
  border: 1px solid rgba(255, 255, 255, 0.5);
  position: relative;
  transition: transform 0.2s ease, box-shadow 0.2s ease, border-color 0.2s ease;
  display: flex;
  flex-direction: column;
  gap: 6px;
  height: 100%;
  max-width: 260px;
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
  margin-bottom: 4px;
  font-weight: 700;
}

.org-item p {
  font-size: 14px;
  color: var(--color-muted);
  margin-bottom: 0;
  line-height: 1.65;
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

.group-detail + .group-detail {
  margin-top: 16px;
}

.group-detail-text {
  display: flex;
  align-items: flex-start;
  gap: 18px;
}

.group-detail-text.reverse {
  flex-direction: row-reverse;
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

.image-nav {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 10px;
  pointer-events: none;
  opacity: 0;
  transition: opacity 0.2s ease;
}

.image-wrapper:hover .image-nav {
  opacity: 1;
}

.nav-btn {
  pointer-events: auto;
  width: 38px;
  height: 38px;
  border-radius: 50%;
  border: none;
  background: rgba(255, 255, 255, 0.9);
  box-shadow: 0 8px 22px rgba(0, 0, 0, 0.18);
  font-size: 18px;
  color: var(--color-text);
  cursor: pointer;
  transition: transform 0.15s ease, background 0.15s ease, box-shadow 0.15s ease;
}

.nav-btn:hover {
  background: #fff;
  transform: scale(1.05);
  box-shadow: 0 12px 28px rgba(0, 0, 0, 0.22);
}

.image-indicator {
  position: absolute;
  bottom: 10px;
  left: 50%;
  transform: translateX(-50%);
  background: rgba(0, 0, 0, 0.55);
  color: #fff;
  padding: 6px 10px;
  border-radius: 999px;
  font-size: 12px;
  letter-spacing: 0.3px;
  pointer-events: none;
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
