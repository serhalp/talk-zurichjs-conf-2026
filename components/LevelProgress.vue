<script setup lang="ts">
import { computed, ref, watch } from "vue";

const props = defineProps<{ level: number }>();
const raised = ref(false);
const title = computed(
  () =>
    [
      "",
      "Static",
      "Static++",
      "Builds",
      "Zero config",
      "Full stack",
      "Frontend cloud",
      "Frontend cloud, hard mode",
      "Frontend cloud, co-op mode",
    ][props.level],
);
watch(
  () => props.level,
  (level, previous) => {
    raised.value = level > previous;
  },
);
</script>

<template>
  <div class="level-progress">
    <div :key="level" :class="{ 'level-up': raised }">
      <LevelBadge :number="level">{{ title }}</LevelBadge>
      <span v-if="raised" class="level-up-label" aria-hidden="true"
        >↑ LEVEL UP!</span
      >
    </div>
  </div>
</template>

<style scoped>
.level-progress {
  position: relative;
  flex-shrink: 0;
}
.level-progress :deep(.level-badge) {
  margin: 0;
}
.level-up {
  animation: level-bounce 650ms cubic-bezier(0.2, 0.8, 0.2, 1) both;
}
.level-up-label {
  position: absolute;
  right: 12px;
  top: -24px;
  color: #bef264;
  font-family: var(--slidev-code-font-family);
  font-size: 16px;
  font-weight: 700;
  letter-spacing: 0.08em;
  white-space: nowrap;
  animation: level-flash 1100ms ease-out both;
}
@keyframes level-bounce {
  0% {
    transform: translateY(5px) scale(0.96);
  }
  35% {
    transform: translateY(-5px) scale(1.06) rotate(-1deg);
    filter: drop-shadow(0 0 10px #bef26480);
  }
  65% {
    transform: translateY(2px) scale(0.99);
  }
  100% {
    transform: none;
    filter: none;
  }
}
@keyframes level-flash {
  0% {
    opacity: 0;
    transform: translateY(7px);
  }
  20%,
  65% {
    opacity: 1;
  }
  100% {
    opacity: 0;
    transform: translateY(-8px);
  }
}
@media (prefers-reduced-motion: reduce) {
  .level-up {
    animation: none;
  }
  .level-up-label {
    animation: none;
    display: none;
  }
}
</style>
