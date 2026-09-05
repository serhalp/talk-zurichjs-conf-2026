<script setup lang="ts">
defineProps<{
  revealed: boolean;
  logos: { name: string; src: string; color?: boolean }[];
}>();
</script>

<template>
  <div class="tool-logos" :class="{ revealed, compact: logos.length > 5 }">
    <div
      v-for="(logo, index) in logos"
      :key="logo.name"
      class="tool-logo"
      :style="{ '--logo-index': index }"
    >
      <img :src="logo.src" alt="" :class="{ monochrome: !logo.color }" />
      <span>{{ logo.name }}</span>
    </div>
  </div>
</template>

<style scoped>
.tool-logos {
  display: flex;
  justify-content: space-between;
  gap: 20px;
  margin-top: 22px;
}
.tool-logo {
  display: flex;
  align-items: center;
  gap: 12px;
  color: #e2e8f0;
  font-size: 24px;
  opacity: 0;
  transform: translateY(12px);
  transition:
    opacity 300ms ease,
    transform 300ms ease;
}
.revealed .tool-logo {
  opacity: 1;
  transform: translateY(0);
  transition-delay: calc(var(--logo-index) * 180ms);
}
.tool-logo img {
  width: 40px;
  height: 40px;
  object-fit: contain;
}
.monochrome {
  filter: brightness(0) invert(1);
}
.compact {
  gap: 12px;
}
.compact .tool-logo {
  gap: 8px;
  font-size: 20px;
  white-space: nowrap;
}
.compact img {
  width: 32px;
  height: 32px;
}
@media (prefers-reduced-motion: reduce) {
  .tool-logo {
    transition: none;
    transform: none;
  }
}
</style>
