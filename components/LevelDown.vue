<script setup lang="ts">
import { onBeforeUnmount, ref, watch } from "vue";

const props = defineProps<{ lost: boolean }>();
const level = ref(props.lost ? 3 : 5);
const dropping = ref(false);
let nextDrop: ReturnType<typeof setTimeout> | undefined;

watch(
  () => props.lost,
  (lost) => {
    clearTimeout(nextDrop);
    dropping.value = lost;
    level.value = lost ? 4 : 5;
    if (lost)
      nextDrop = setTimeout(() => {
        level.value = 3;
      }, 800);
  },
);
onBeforeUnmount(() => clearTimeout(nextDrop));
</script>

<template>
  <div class="level-loss">
    <div :key="level" :class="{ dropping }">
      <LevelBadge :number="level">
        <span class="ability">Full stack</span>
        <span class="ability zero-config" :class="{ lost }">Zero config</span>
      </LevelBadge>
      <span v-if="dropping" class="down-label" aria-hidden="true"
        >↓ LEVEL DOWN!</span
      >
    </div>
  </div>
</template>

<style scoped>
.level-loss {
  position: relative;
  width: fit-content;
  margin-bottom: 8px;
}
.level-loss :deep(.level-badge) {
  margin: 0;
}
.level-loss :deep(.level-title) {
  display: flex;
  padding: 0;
}
.ability {
  padding: 7px 20px 7px 16px;
}
.zero-config {
  position: relative;
  border-left: 1px solid #bef26466;
}
.zero-config::after {
  content: "";
  position: absolute;
  top: 50%;
  left: 12px;
  right: 16px;
  height: 3px;
  background: #f7fee7;
  transform: scaleX(0);
  transform-origin: left;
  transition: transform 250ms ease-out;
}
.zero-config.lost::after {
  transform: scaleX(1);
}
.dropping {
  animation: drop 650ms ease-out both;
}
.down-label {
  position: absolute;
  top: -24px;
  right: 12px;
  color: #f0abfc;
  font-family: var(--slidev-code-font-family);
  font-size: 16px;
  font-weight: 700;
  letter-spacing: 0.08em;
  animation: down-flash 750ms ease-out both;
}
@keyframes drop {
  0% {
    transform: translateY(-5px);
  }
  35% {
    transform: translateY(5px) rotate(1deg);
    filter: drop-shadow(0 0 8px #f0abfc70);
  }
  65% {
    transform: translateY(-2px);
  }
  100% {
    transform: none;
  }
}
@keyframes down-flash {
  0% {
    opacity: 0;
    transform: translateY(-6px);
  }
  20%,
  65% {
    opacity: 1;
  }
  100% {
    opacity: 0;
    transform: translateY(8px);
  }
}
@media (prefers-reduced-motion: reduce) {
  .dropping {
    animation: none;
  }
  .down-label {
    display: none;
  }
  .zero-config::after {
    transition: none;
  }
}
</style>
