<script setup lang="ts">
defineProps<{ number: number }>();
</script>

<template>
  <h2 class="level-badge">
    <span class="level-number">LEVEL {{ number }}</span>
    <span class="level-title"><slot /></span>
  </h2>
</template>

<style scoped>
.level-badge {
  display: flex;
  width: fit-content;
  margin: 0 0 8px;
  padding: 0;
  overflow: hidden;
  background: #202b18;
  border-bottom: 2px solid #bef264;
  clip-path: polygon(0 0, calc(100% - 10px) 0, 100% 10px, 100% 100%, 0 100%);
  font-family: var(--slidev-code-font-family);
  line-height: 1;
}

.level-number {
  padding: 9px 12px;
  background: #bef264;
  color: #16200c;
  font-size: 18px;
  font-weight: 700;
  letter-spacing: 0.06em;
}

.level-title {
  padding: 7px 20px 7px 16px;
  color: #f7fee7;
  font-size: 22px;
  font-weight: 400;
}
</style>
