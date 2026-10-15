<script setup>
defineProps({ name: { type: String, default: 'arrow' }, size: { type: [Number, String], default: 20 } });

// 自绘线性图标，不请求外部图标服务。
const paths = {
  arrow: 'M5 12h14m-6-6 6 6-6 6',
  diagonal: 'M6 18 18 6M6 6h12v12',
  down: 'm6 9 6 6 6-6',
  up: 'm6 14 6-6 6 6',
  sun: 'M12 2v2m0 16v2M2 12h2m16 0h2M5 5l1.5 1.5m11 11L19 19M5 19l1.5-1.5m11-11L19 5M16 12a4 4 0 1 1-8 0 4 4 0 0 1 8 0',
  moon: 'M20 15.2A8.4 8.4 0 0 1 8.8 4 8.5 8.5 0 1 0 20 15.2Z',
  menu: 'M4 6h16M4 12h16M4 18h16',
  close: 'm6 6 12 12M6 18 18 6',
  code: 'm8 6-6 6 6 6m8-12 6 6-6 6m-3-15-2 18',
  layers: 'm12 3 10 5-10 5L2 8l10-5Zm-10 9 10 5 10-5M2 16l10 5 10-5',
  network: 'M9 3h6v6H9zM2 16h6v6H2zm14 0h6v6h-6zM12 9v4M5 16v-3h14v3',
  terminal: 'M3 4h18v16H3zM7 9l3 3-3 3m6 0h4',
  sparkles: 'm12 2 2.5 7.5L22 12l-7.5 2.5L12 22l-2.5-7.5L2 12l7.5-2.5L12 2ZM20 2v4m-2-2h4',
  users: 'M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2M22 21v-2a4 4 0 0 0-3-3.9M16 3.1a4 4 0 0 1 0 7.8M13 7a4 4 0 1 1-8 0 4 4 0 0 1 8 0',
  trophy: 'M8 3h8v7a4 4 0 0 1-8 0V3Zm0 2H4v3a4 4 0 0 0 4 4m8-7h4v3a4 4 0 0 1-4 4m-4 2v5m-5 2h10',
  game: 'M7 7h10a4 4 0 0 1 4 3l1 7a2 2 0 0 1-3.4 1.7L16 16H8l-2.6 2.7A2 2 0 0 1 2 17l1-7a4 4 0 0 1 4-3Zm0 3v4m-2-2h4m7-1h.01M18 13h.01',
  music: 'M9 18V5l12-2v13M9 8l12-2M9 18a3 3 0 1 1-6 0 3 3 0 0 1 6 0m12-2a3 3 0 1 1-6 0 3 3 0 0 1 6 0',
  compass: 'M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0ZM16 8l-3 5-5 3 3-5 5-3Z',
  school: 'm2 9 10-6 10 6-10 6L2 9Zm4 3v6l6 3 6-3v-6m4-3v8',
  pin: 'M19 10c0 5-7 11-7 11S5 15 5 10a7 7 0 1 1 14 0Zm-5 0a2 2 0 1 1-4 0 2 2 0 0 1 4 0',
  flag: 'M4 22V3m0 0c5-4 11 4 16 0v12c-5 4-11-4-16 0',
  check: 'm5 12 4 4L19 6',
};
</script>

<template>
  <svg :width="size" :height="size" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
    <path :d="paths[name] || paths.arrow" />
  </svg>
</template>
