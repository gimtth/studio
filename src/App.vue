<template>
  <div>
    <template v-if="hasEntered">
      <Navbar :current-section="currentSection" @change-section="changeSection" />
      <component :is="currentView" />
      <FooterSection />
    </template>
    <template v-else>
      <AerialLanding @enter-main="enterMain" />
    </template>
  </div>
</template>

<script setup lang="ts">
import { computed, onBeforeUnmount, onMounted, ref } from 'vue'
import Navbar from './components/Navbar.vue'
import AerialLanding from './components/AerialLanding.vue'
import BannerSection from './components/BannerSection.vue'
import ServicesSection from './components/ServicesSection.vue'
import AboutSection from './components/AboutSection.vue'
import ActivitiesSection from './components/ActivitiesSection.vue'
import RecruitmentSection from './components/RecruitmentSection.vue'
import NetworkSection from './components/NetworkSection.vue'
import FooterSection from './components/FooterSection.vue'

const currentSection = ref<'home' | 'services' | 'about' | 'activities' | 'recruitment' | 'network'>('home')
const hasEntered = ref(false)

const sectionMap = {
  home: BannerSection,
  services: ServicesSection,
  about: AboutSection,
  activities: ActivitiesSection,
  recruitment: RecruitmentSection,
  network: NetworkSection,
}

const currentView = computed(() => sectionMap[currentSection.value] || BannerSection)

const changeSection = (id: string) => {
  if (id in sectionMap) {
    currentSection.value = id as keyof typeof sectionMap
  }
}

const enterMain = () => {
  hasEntered.value = true
}

const handleMessage = (event: MessageEvent) => {
  if (event.data && event.data.type === 'enter-main') {
    hasEntered.value = true
  }
}

onMounted(() => {
  window.addEventListener('message', handleMessage)
})

onBeforeUnmount(() => {
  window.removeEventListener('message', handleMessage)
})
</script>

<style>
@import url('https://cdn.bootcdn.net/ajax/libs/font-awesome/6.4.0/css/all.min.css');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: var(--font-body);
}

body {
  color: var(--color-text);
}

a {
  text-decoration: none;
  color: inherit;
}

.container {
  width: 1200px;
  margin: 0 auto;
  padding: 0 24px;
}

@media (max-width: 1200px) {
  .container {
    width: 100%;
  }
}

.btn {
  display: inline-block;
  padding: 12px 26px;
  background: linear-gradient(135deg, var(--color-primary), var(--color-secondary));
  color: #fff !important;
  border-radius: var(--radius-md);
  transition: all 0.35s ease;
  border: none;
  cursor: pointer;
  font-size: 16px;
  font-weight: 600;
  box-shadow: var(--shadow-card);
}

.btn:hover {
  transform: translateY(-4px) scale(1.01);
  box-shadow: var(--shadow-soft);
}

.section-title {
  text-align: center;
  margin-bottom: 64px;
  max-width: 820px;
  margin-left: auto;
  margin-right: auto;
}

.section-title h2 {
  font-size: 32px;
  color: var(--color-primary);
  margin-bottom: 10px;
  position: relative;
  display: inline-block;
  letter-spacing: 0.8px;
}

.section-title h2::after {
  content: '';
  position: absolute;
  bottom: -10px;
  left: 50%;
  transform: translateX(-50%);
  width: 80px;
  height: 4px;
  background: linear-gradient(90deg, var(--color-primary), var(--color-secondary));
  border-radius: 10px;
}

.section-title p {
  font-size: 16px;
  color: var(--color-muted);
  max-width: 800px;
  margin: 0 auto;
}

section {
  padding: 96px 0;
}

@media (max-width: 992px) {
  section {
    padding: 80px 0;
  }
}

@media (max-width: 768px) {
  section {
    padding: 72px 0;
  }
}
</style>
