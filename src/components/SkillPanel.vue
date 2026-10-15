<script setup>
import { computed, ref } from 'vue';
import AppIcon from './AppIcon.vue';
import SectionHeading from './SectionHeading.vue';
import { skills } from '../data/profile';

const selectedId = ref(skills[0].id);
const selected = computed(() => skills.find((skill) => skill.id === selectedId.value));
const groups = [{ id: 'foundation', name: '当前技术基础', label: 'FOUNDATION' }, { id: 'growth', name: '希望进一步提升', label: 'TO EXPLORE' }];

// 方向键切换标签；鼠标与键盘使用同一份响应式状态。
function onTabKey(event, index) {
  let next = index;
  if (event.key === 'ArrowDown' || event.key === 'ArrowRight') next = (index + 1) % skills.length;
  else if (event.key === 'ArrowUp' || event.key === 'ArrowLeft') next = (index - 1 + skills.length) % skills.length;
  else if (event.key === 'Home') next = 0;
  else if (event.key === 'End') next = skills.length - 1;
  else return;
  event.preventDefault();
  selectedId.value = skills[next].id;
  document.getElementById(`skill-tab-${selectedId.value}`)?.focus();
}
</script>

<template>
  <section id="skills" class="section section-tinted page-section" aria-labelledby="skills-title">
    <div class="container">
      <SectionHeading number="02" english="SKILL INVENTORY" title="我的技能，持续加载中" description="如实记录起点，把想学的事情一步步变成能力。" />
      <h3 id="skills-title" class="sr-only">技能面板与技术基础</h3>
      <div class="skill-layout reveal">
        <div class="skill-tabs" role="tablist" aria-label="选择技能查看学习状态" aria-orientation="vertical">
          <div v-for="group in groups" :key="group.id" class="skill-group" role="presentation">
            <p class="skill-group-label">{{ group.name }}<span class="mono">{{ group.label }}</span>
            </p>
            <button v-for="skill in skills.filter((item) => item.category === group.id)" :id="`skill-tab-${skill.id}`" :key="skill.id" class="skill-tab" :class="{ selected: selectedId === skill.id }" role="tab" :aria-selected="selectedId === skill.id" aria-controls="skill-detail" :tabindex="selectedId === skill.id ? 0 : -1" @click="selectedId = skill.id" @keydown="onTabKey($event, skills.indexOf(skill))">
              <AppIcon :name="skill.icon" :size="20" />
              <span>{{ skill.shortLabel }}</span>
              <span class="skill-tab-status">{{ skill.status }}</span>
              <AppIcon name="arrow" :size="15" />
            </button>
          </div>
        </div>
        <div id="skill-detail" class="skill-detail surface" role="tabpanel" :aria-labelledby="`skill-tab-${selectedId}`" tabindex="0">
          <div class="skill-detail-top">
            <span class="mono">SELECTED ABILITY / {{ String(skills.indexOf(selected) + 1).padStart(2, '0') }}</span>
            <span class="status-tag" :class="{ 'status-cyan': selected.category === 'foundation' }">
              <span class="status-dot">
              </span>{{ selected.status }}</span>
          </div>
          <Transition name="detail" mode="out-in">
            <div :key="selectedId" class="skill-detail-content">
              <div class="skill-large-icon">
                <AppIcon :name="selected.icon" :size="38" />
              </div>
              <h3>{{ selected.title }}</h3>
              <p class="skill-summary">{{ selected.summary }}</p>
              <p class="skill-description">{{ selected.description }}</p>
              <div class="next-actions">
                <span class="detail-label">下一步 · 学习行动</span>
                <ul>
                  <li v-for="action in selected.actions" :key="action">
                    <span class="list-mark" aria-hidden="true">↗</span>{{ action }}</li>
                </ul>
              </div>
            </div>
          </Transition>
          <div class="skill-footnote">
            <AppIcon name="compass" :size="16" />
            <span>学习状态是记录，不是能力排名。</span>
          </div>
        </div>
      </div>
      <p class="section-note">
        <span class="tiny-square">
        </span> 本站使用 Vue 3 完成本次考核；未来的专业方向，仍在学习与实践中探索。</p>
    </div>
  </section>
</template>
