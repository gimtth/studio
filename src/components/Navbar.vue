<template>
  <nav class="navbar">
    <div class="container navbar-content">
      <div class="logo">
        <img src="/logo.png" alt="升达网络技术工作室Logo" />
        <h1>升达网络技术工作室</h1>
      </div>
      <ul class="nav-menu" ref="navMenu">
        <li v-for="item in navItems" :key="item.id">
          <a
            href="#"
            :class="{ active: currentSection === item.id }"
            @click.prevent="go(item.id)"
          >
            {{ item.label }}
          </a>
        </li>
      </ul>
      <div class="mobile-menu-btn" ref="mobileMenuBtn" @click="toggleMobileMenu">
        <i class="fas fa-bars"></i>
      </div>
    </div>
  </nav>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const props = defineProps<{
  currentSection: string
}>()

const emit = defineEmits<{
  (e: 'change-section', id: string): void
}>()

const navItems = [
  { id: 'home', label: '首页' },
  { id: 'about', label: '兴趣小组' },
  { id: 'services', label: '服务中心' },
  { id: 'activities', label: '活动动态' },
  { id: 'recruitment', label: '招新专栏' },
  { id: 'network', label: '校园网服务' },
]

const navMenu = ref<HTMLElement | null>(null)
const mobileMenuBtn = ref<HTMLElement | null>(null)

const toggleMobileMenu = () => {
  navMenu.value?.classList.toggle('active')
  const isActive = navMenu.value?.classList.contains('active')
  mobileMenuBtn.value && (mobileMenuBtn.value.innerHTML = `<i class="fas fa-${isActive ? 'times' : 'bars'}"></i>`)
}

const go = (id: string) => {
  emit('change-section', id)
  navMenu.value?.classList.remove('active')
  mobileMenuBtn.value && (mobileMenuBtn.value.innerHTML = '<i class="fas fa-bars"></i>')
}
</script>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background: rgba(255, 255, 255, 0.65);
  border-bottom: 1px solid rgba(255, 255, 255, 0.35);
  box-shadow: var(--shadow-card);
  z-index: 999;
}

.navbar-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 80px;
}

.logo {
  display: flex;
  align-items: center;
}

.logo img {
  height: 50px;
  margin-right: 15px;
}

.logo h1 {
  font-size: 22px;
  color: var(--color-primary);
  letter-spacing: 0.5px;
}

.nav-menu {
  display: flex;
  list-style: none;
}

.nav-menu li {
  margin-left: 30px;
}

.nav-menu a {
  font-size: 15px;
  color: var(--color-text);
  transition: color 0.3s, opacity 0.3s;
  font-weight: 600;
  opacity: 0.82;
}

.nav-menu a:hover,
.nav-menu a.active {
  color: var(--color-primary);
  opacity: 1;
  text-shadow: 0 6px 20px rgba(255, 111, 97, 0.35);
}

.mobile-menu-btn {
  display: none;
  font-size: 24px;
  cursor: pointer;
}

@media (max-width: 768px) {
  .nav-menu {
    position: fixed;
    top: 80px;
    left: -100%;
    flex-direction: column;
    background-color: rgba(255, 255, 255, 0.92);
    width: 100%;
    height: calc(100vh - 80px);
    transition: 0.3s;
    padding: 20px;
  }

  .nav-menu li {
    margin: 15px 0;
  }

  .nav-menu.active {
    left: 0;
  }

  .mobile-menu-btn {
    display: block;
  }
}
</style>
