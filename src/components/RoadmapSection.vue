<script setup>
import { ref } from 'vue';
import AppIcon from './AppIcon.vue';
import SectionHeading from './SectionHeading.vue';
import { roadmap } from '../data/profile';

// 数组记录展开的阶段，允许同时阅读多个阶段。
const openStages = ref([roadmap[0].id]);
const isOpen = (id) => openStages.value.includes(id);
function toggleStage(id) {
  openStages.value = isOpen(id) ? openStages.value.filter((item) => item !== id) : [...openStages.value, id];
}
</script>

<template>
  <section id="roadmap" class="section page-section" aria-labelledby="roadmap-title">
    <div class="container">
      <SectionHeading number="03" english="MAIN QUEST" title="关于未来，认真走好每一步" description="方向可以慢慢清晰，准备从现在开始。" />
      <h3 id="roadmap-title" class="sr-only">未来规划与保研方向</h3>
      <div class="roadmap-layout reveal">
        <aside class="roadmap-purpose">
          <span class="outline-label mono">MY NEXT CHAPTER</span>
          <h3>打好基础，<br />争取<span class="accent">继续深造</span>。</h3>
          <p>我目前的主要目标是争取保研，在计算机相关领域继续深入学习，并逐渐找到适合自己的发展方向。</p>
          <p>选择这条路，是因为我希望给自己更扎实的专业基础和更充分的探索空间。课程学习帮助我建立知识体系，项目、竞赛和科研实践则能帮助我理解知识如何解决实际问题。</p>
          <div class="long-term-goal">
            <AppIcon name="flag" :size="24" />
            <div>
              <span>长期目标</span>
              <strong>争取获得保研机会</strong>
              <p>持续学习 · 积累实践 · 探索方向</p>
            </div>
          </div>
          <p class="planning-note">以下为行动规划，未来目标仍需一步步完成。</p>
        </aside>
        <div class="timeline">
          <article v-for="(stage, index) in roadmap" :key="stage.id" class="timeline-item" :class="{ 'is-expanded': isOpen(stage.id) }">
            <span class="timeline-node" :class="{ current: index === 0 }" aria-hidden="true">{{ stage.number }}</span>
            <div class="timeline-card">
              <button :id="`stage-trigger-${stage.id}`" class="stage-toggle" :aria-expanded="isOpen(stage.id)" :aria-controls="`stage-content-${stage.id}`" @click="toggleStage(stage.id)">
                <span class="stage-heading">
                  <span class="stage-meta">
                    <span class="mono">PHASE {{ stage.number }}</span>
                    <span class="stage-status" :class="{ current: index === 0 }">{{ stage.status }}</span>
                  </span>
                  <span class="stage-title">{{ stage.title }}</span>
                  <span class="stage-subtitle">{{ stage.subtitle }}</span>
                </span>
                <span class="stage-expand" aria-hidden="true">{{ isOpen(stage.id) ? '−' : '+' }}</span>
              </button>
              <div :id="`stage-content-${stage.id}`" class="action-collapse" :class="{ open: isOpen(stage.id) }" :inert="!isOpen(stage.id)" :aria-hidden="!isOpen(stage.id)" role="region" :aria-labelledby="`stage-trigger-${stage.id}`">
                <div class="action-collapse-inner">
                  <div class="stage-actions">
                    <p>{{ stage.description }}</p>
                    <ul>
                      <li v-for="action in stage.actions" :key="action">
                        <span class="action-bullet" aria-hidden="true">
                        </span>{{ action }}</li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>
          </article>
        </div>
      </div>
    </div>
  </section>
</template>
