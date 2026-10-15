<script setup>
import AppIcon from './AppIcon.vue';
import SectionHeading from './SectionHeading.vue';
import { clubGoals } from '../data/profile';
</script>

<template>
  <section id="club" class="section section-tinted club-section page-section" aria-labelledby="club-title">
    <div class="container">
      <SectionHeading number="04" english="SIDE QUESTS, REAL GROWTH" title="与同行者一起，把想法变成实践" description="我想在 JAVA 俱乐部收获的，不止是知识。" />
      <h3 id="club-title" class="sr-only">加入俱乐部的原因与具体学习目标</h3>
      <div class="club-intro reveal">
        <div class="club-intro-label">
          <span class="tiny-square">
          </span>
          <span>为什么加入<br />
            <strong>JAVA 俱乐部</strong>
          </span>
        </div>
        <div>
          <p>我希望接触课堂之外的软件开发、学科竞赛和科研实践，也想学会更有效地使用 AI 工具。参与真实项目，能让我了解一个想法从构思到实现的过程；学习提问、判断和验证，才能让 AI 真正帮助自己理解与解决问题。</p>
          <p>也期待认识志同道合的同学，向有经验的学长学姐请教，在交流和合作中积累经验，逐渐找到适合自己的方向。</p>
        </div>
      </div>
      <div class="club-goals reveal">
        <article v-for="goal in clubGoals" :key="goal.number" class="goal-card surface">
          <div class="goal-top">
            <span class="goal-icon">
              <AppIcon :name="goal.icon" :size="24" />
            </span>
            <span class="mono">QUEST {{ goal.number }}</span>
            <span class="goal-state">学习目标</span>
          </div>
          <p class="goal-english mono">{{ goal.english }}</p>
          <h3>{{ goal.title }}</h3>
          <p class="goal-description">{{ goal.description }}</p>
          <ul>
            <li v-for="action in goal.actions" :key="action">
              <span class="list-mark" aria-hidden="true">+</span>{{ action }}</li>
          </ul>
          <div class="goal-outcome">
            <span>期待收获</span>
            <p>{{ goal.outcome }}</p>
          </div>
        </article>
      </div>
      <div class="closing-line">
        <span class="mono">THE JOURNEY CONTINUES</span>
        <p>保持好奇，踏实前行。<br class="mobile-break" />下一段成长，期待一起出发<span class="accent">。</span>
        </p>
        <span class="closing-star" aria-hidden="true">✳</span>
      </div>
    </div>
  </section>
</template>
