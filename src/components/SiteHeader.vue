<script setup>
import { nextTick, ref, watch } from 'vue';
import AppIcon from './AppIcon.vue';

const props = defineProps({ theme: String, activeSection: String });
defineEmits(['toggle-theme']);
const menuOpen = ref(false);
const menuButton = ref(null);
const links = [
  { id: 'profile', title: '个人档案', number: '00' },
  { id: 'about', title: '关于我', number: '01' },
  { id: 'skills', title: '技能面板', number: '02' },
  { id: 'roadmap', title: '未来规划', number: '03' },
  { id: 'club', title: '俱乐部目标', number: '04' },
];

watch(() => props.activeSection, () => { menuOpen.value = false; });
async function toggleMenu() {
  menuOpen.value = !menuOpen.value;
  if (menuOpen.value) {
    await nextTick();
    document.querySelector('#primary-navigation .active')?.focus();
  }
}
function closeWithEscape(event) {
  if (event.key === 'Escape' && menuOpen.value) {
    menuOpen.value = false;
    menuButton.value?.focus();
  }
}
</script>

<template>
  <header class="site-header" @keydown="closeWithEscape">
    <div class="header-inner">
      <a class="brand" href="#profile" aria-label="杨照轩，返回个人档案" @click="menuOpen = false">
        <span class="brand-mark">Z<span>·</span>
        </span>
        <span class="brand-copy">YZX<span>PERSONAL ARCHIVE</span>
        </span>
      </a>
      <nav id="primary-navigation" class="navigation" :class="{ 'is-open': menuOpen }" aria-label="主导航">
        <a v-for="link in links" :key="link.id" :href="`#${link.id}`" :class="{ active: activeSection === link.id }" :aria-current="activeSection === link.id ? 'location' : undefined" @click="menuOpen = false">
          <span class="nav-number">{{ link.number }}</span>{{ link.title }}
        </a>
      </nav>
      <div class="header-actions">
        <button class="theme-toggle" :aria-label="theme === 'dark' ? '切换到浅色主题' : '切换到深色主题'" @click="$emit('toggle-theme')">
          <AppIcon :name="theme === 'dark' ? 'sun' : 'moon'" :size="18" />
          <span>{{ theme === 'dark' ? '浅色' : '深色' }}</span>
        </button>
        <button ref="menuButton" class="menu-toggle icon-button" :aria-expanded="menuOpen" aria-controls="primary-navigation" :aria-label="menuOpen ? '关闭导航菜单' : '打开导航菜单'" @click="toggleMenu">
          <AppIcon :name="menuOpen ? 'close' : 'menu'" />
        </button>
      </div>
    </div>
  </header>
</template>
