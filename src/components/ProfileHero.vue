<script setup>
import AppIcon from './AppIcon.vue';
import { profile } from '../data/profile';
</script>

<template>
  <section id="profile" class="hero page-section" aria-labelledby="profile-title">
    <div class="hero-grid" aria-hidden="true">
    </div>
    <div class="container hero-content">
      <div class="hero-copy">
        <div class="hero-status">
          <span class="status-dot">
          </span> 保持好奇，持续探索 <span class="mono">/ PROFILE 001</span>
        </div>
        <p class="hero-kicker mono">HELLO WORLD. THIS IS ME.</p>
        <h1 id="profile-title">我是<span>{{ profile.name }}</span>
          <span class="hero-period">.</span>
        </h1>
        <p class="hero-english mono">{{ profile.englishName }}</p>
        <p class="hero-identity">
          <AppIcon name="school" :size="18" />{{ profile.school }}<span class="divider">
          </span>{{ profile.major }} · {{ profile.year }}</p>
        <p class="hero-intro">{{ profile.intro }}<br />一个喜欢游戏、音乐，也对计算机世界充满好奇的普通学生。</p>
        <div class="hero-tags">
          <span v-for="word in profile.keywords" :key="word">
            <i>#</i> {{ word }}</span>
        </div>
        <div class="hero-buttons">
          <a href="#about" class="button button-primary">读取我的档案 <AppIcon name="arrow" :size="18" />
          </a>
          <a href="#roadmap" class="button button-secondary">探索未来计划 <AppIcon name="diagonal" :size="17" />
          </a>
        </div>
        <div class="hero-caption">
          <span class="small-cross">+</span> 关于我与我的未来<span class="caption-line">
          </span>
          <span class="mono">A STORY IN PROGRESS</span>
        </div>
      </div>
      <div class="identity-panel">
        <div class="panel-topline">
          <span class="mono">PLAYER PROFILE</span>
          <span class="panel-status">
            <span class="status-dot">
            </span> 探索中</span>
        </div>
        <div class="emblem-stage">
          <span class="coordinate coordinate-top mono" aria-hidden="true">WUST / NE</span>
          <span class="coordinate coordinate-side mono" aria-hidden="true">KEEP EXPLORING</span>
          <svg class="emblem-orbits" viewBox="0 0 400 320" fill="none" aria-hidden="true">
            <circle cx="200" cy="160" r="128" stroke="currentColor" stroke-dasharray="2 8" />
            <circle cx="200" cy="160" r="112" stroke="currentColor" opacity=".35" />
            <path d="M91 84a133 133 0 0 1 213-4M308 236a133 133 0 0 1-211 10" stroke="currentColor" stroke-width="2" />
            <path d="M38 160h42m240 0h42M200 10v26m0 248v26" stroke="currentColor" />
            <path d="M54 46h19M63.5 36.5v19m263 219h19m-9.5-9.5v19" stroke="currentColor" />
            <circle cx="305" cy="81" r="4" fill="currentColor" />
            <circle cx="98" cy="245" r="3" fill="currentColor" />
          </svg>
          <img v-if="profile.avatar" class="profile-avatar" :src="profile.avatar" :alt="`${profile.name}的个人头像`" />
          <div v-else class="crystal-emblem" role="img" aria-label="原创 YZX 几何档案徽章，个人头像待补充">
            <div class="crystal-back">
            </div>
            <div class="crystal-front">
              <span>Y<span class="emblem-slash">/</span>Z</span>
            </div>
            <span class="crystal-spark">
            </span>
          </div>
          <span class="emblem-label mono">YZX <span>//</span> EXPLORER</span>
        </div>
        <div class="identity-name">
          <div>
            <h2>{{ profile.name }}</h2>
            <p>{{ profile.college }}</p>
          </div>
          <span class="identity-symbol" aria-hidden="true">↗</span>
        </div>
        <div class="identity-facts">
          <div>
            <span>专业方向</span>
            <strong>{{ profile.major }}</strong>
          </div>
          <div>
            <span>所在班级</span>
            <strong>{{ profile.className }}</strong>
          </div>
          <div>
            <span>当前年级</span>
            <strong>{{ profile.year }}</strong>
          </div>
        </div>
        <div class="panel-bottomline">
          <span class="mono">AVATAR / {{ profile.avatar ? 'PERSONAL' : 'PLACEHOLDER' }}</span>
          <span>{{ profile.avatar ? '个人头像' : '几何徽章 · 头像待补充' }}</span>
        </div>
        <span class="panel-corner" aria-hidden="true">
        </span>
      </div>
    </div>
    <div class="container hero-bottom">
      <a href="#about">
        <span class="scroll-cue" aria-hidden="true">
        </span>
        <span class="mono">SCROLL TO DISCOVER</span>
      </a>
      <span>每一次尝试，都是下一步的起点。<span class="small-cross">+</span>
      </span>
    </div>
  </section>
</template>
