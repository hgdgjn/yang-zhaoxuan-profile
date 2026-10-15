<script setup>
defineProps({ number: String, english: String, title: String, description: String });
</script>

<template>
  <header class="section-heading">
    <div>
      <p class="eyebrow">
        <span class="section-number">{{ number }}</span> {{ english }}</p>
      <h2>{{ title }}<span class="heading-dot">.</span>
      </h2>
    </div>
    <p v-if="description" class="section-description">{{ description }}</p>
  </header>
</template>
