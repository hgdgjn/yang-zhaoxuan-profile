<script setup>
import AppIcon from './AppIcon.vue';
import SectionHeading from './SectionHeading.vue';
import { profile } from '../data/profile';
const interests = [{ icon: 'game', name: '游戏', note: '享受投入与探索' }, { icon: 'music', name: '音乐', note: '给日常一点节奏' }, { icon: 'terminal', name: '计算机技术', note: '想知道它如何实现' }];
</script>

<template>
  <section id="about" class="section page-section" aria-labelledby="about-title">
    <div class="container">
      <SectionHeading number="01" english="CHARACTER FILE" title="不止一面，都是我" description="从课堂到生活，慢慢拼出自己的轮廓。" />
      <h3 id="about-title" class="sr-only">关于我与人物资料</h3>
      <div class="about-grid reveal">
        <article class="about-intro surface">
          <div class="card-eyebrow">
            <span class="tiny-square">
            </span> 人物资料 <span class="mono">ABOUT ME</span>
          </div>
          <h3>不急着定义方向，<br />先认真积累<span class="accent">。</span>
          </h3>
          <p>我是{{ profile.name }}，来自{{ profile.school }}{{ profile.college }}，目前就读于{{ profile.className }}，是一名{{ profile.year }}学生。</p>
          <p>我愿意主动学习新事物，也希望把课堂上的知识用到实践中。面对感兴趣的问题，我想多问一句“为什么”，再试着自己找到答案。</p>
          <div class="about-signature">
            <span class="mono">CURIOUS BY NATURE</span>
            <AppIcon name="compass" :size="28" />
          </div>
        </article>
        <div class="about-right">
          <article class="interest-panel surface">
            <div class="card-eyebrow">兴趣坐标<span class="mono">OFFLINE & ONLINE</span>
            </div>
            <div class="interest-list">
              <div v-for="interest in interests" :key="interest.name">
                <span class="interest-icon">
                  <AppIcon :name="interest.icon" :size="23" />
                </span>
                <h3>{{ interest.name }}</h3>
                <p>{{ interest.note }}</p>
              </div>
            </div>
          </article>
          <article class="experience-panel surface">
            <div class="card-eyebrow">校园经历<span class="mono">CAMPUS EXPERIENCE</span>
            </div>
            <div class="experience-body">
              <span class="experience-icon">
                <AppIcon name="users" :size="25" />
              </span>
              <div>
                <h3>团支书 <span class="muted">/</span> 新生班助</h3>
                <p>参与过班级事务及学生工作。在与同学沟通、配合的过程中积累经验，也希望继续提升组织与团队协作能力。</p>
              </div>
            </div>
          </article>
        </div>
      </div>
      <div class="character-strip reveal">
        <span class="mono">PERSONAL TRAITS</span>
        <span>
          <i>01</i> 主动学习</span>
        <span>
          <i>02</i> 乐于探索</span>
        <span>
          <i>03</i> 重视实践</span>
        <span>
          <i>04</i> 学会独立解决问题</span>
      </div>
    </div>
  </section>
</template>
