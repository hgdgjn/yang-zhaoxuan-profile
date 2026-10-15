<script setup>
import { onMounted, onUnmounted, ref, watch } from 'vue';
import SiteHeader from './components/SiteHeader.vue';
import ProfileHero from './components/ProfileHero.vue';
import AboutSection from './components/AboutSection.vue';
import SkillPanel from './components/SkillPanel.vue';
import RoadmapSection from './components/RoadmapSection.vue';
import ClubSection from './components/ClubSection.vue';
import AppIcon from './components/AppIcon.vue';
import { profile } from './data/profile';

const theme = ref(document.documentElement.dataset.theme === 'light' ? 'light' : 'dark');
const activeSection = ref('profile');
const showBackToTop = ref(false);
let revealObserver;
let scrollFrame = 0;
let sections = [];

watch(theme, (value) => {
  document.documentElement.dataset.theme = value;
  document.querySelector('meta[name="theme-color"]')?.setAttribute('content', value === 'dark' ? '#0b1019' : '#f3f5fb');
  try { localStorage.setItem('yzx-profile-theme', value); } catch { /* 隐私模式下仍允许切换主题 */ }
}, { immediate: true });

// 用一帧合并连续滚动事件，根据页面实际位置同步导航，避免只在点击时更新。
function updateScrollState() {
  const marker = Math.min(window.innerHeight * 0.32, 230);
  let current = sections[0]?.id || 'profile';
  for (const section of sections) {
    if (section.getBoundingClientRect().top <= marker) current = section.id;
  }
  if (window.scrollY + window.innerHeight >= document.documentElement.scrollHeight - 8) current = 'club';
  activeSection.value = current;
  showBackToTop.value = window.scrollY > 600;
  scrollFrame = 0;
}
function onScroll() {
  if (!scrollFrame) scrollFrame = window.requestAnimationFrame(updateScrollState);
}

onMounted(() => {
  sections = [...document.querySelectorAll('.page-section')];
  window.addEventListener('scroll', onScroll, { passive: true });
  window.addEventListener('resize', onScroll);
  updateScrollState();
  // 内容默认可见；只有支持观察器且未要求减少动画时，才启用滚动渐入。
  if ('IntersectionObserver' in window && !window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
    revealObserver = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('is-visible');
          revealObserver.unobserve(entry.target);
        }
      });
    }, { threshold: 0.06 });
    document.querySelectorAll('.reveal').forEach((element) => {
      if (element.getBoundingClientRect().top >= window.innerHeight) {
        element.classList.add('will-reveal');
        revealObserver.observe(element);
      }
    });
  }
});

onUnmounted(() => {
  window.removeEventListener('scroll', onScroll);
  window.removeEventListener('resize', onScroll);
  window.cancelAnimationFrame(scrollFrame);
  revealObserver?.disconnect();
});
</script>

<template>
  <a class="skip-link" href="#main-content">跳转到主要内容</a>
  <SiteHeader :theme="theme" :active-section="activeSection" @toggle-theme="theme = theme === 'dark' ? 'light' : 'dark'" />
  <main id="main-content" tabindex="-1">
    <ProfileHero />
    <AboutSection />
    <SkillPanel />
    <RoadmapSection />
    <ClubSection />
  </main>
  <footer class="site-footer">
    <div class="container footer-main">
      <a class="footer-name" href="#profile">{{ profile.name }}<span class="mono">YANG ZHAOXUAN</span>
      </a>
      <p>{{ profile.school }} · {{ profile.major }}<span>关于我与我的未来 · JAVA 俱乐部招新考核</span>
      </p>
      <span class="qq-placeholder">QQ：{{ profile.qq || '待补充' }}</span>
      <a class="footer-top" href="#profile">返回顶部<AppIcon name="up" :size="17" />
      </a>
    </div>
    <div class="container footer-bottom">
      <span class="mono">DESIGNED TO EXPLORE. BUILT TO GROW.</span>
      <span>Vue 3 + Vite <span class="small-cross">+</span> 持续学习中</span>
    </div>
  </footer>
  <a v-show="showBackToTop" class="floating-top icon-button" href="#profile" aria-label="返回页面顶部">
    <AppIcon name="up" :size="21" />
  </a>
</template>
