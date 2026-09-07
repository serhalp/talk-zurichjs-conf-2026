<script setup lang="ts">
defineProps<{ active: boolean }>();

const colors = [
  "#bef264",
  "#67e8f9",
  "#c4b5fd",
  "#fcd34d",
  "#fda4af",
  "#5eead4",
];
</script>

<template>
  <div
    class="co-op-players"
    :class="{ active }"
    role="list"
    aria-label="Players"
  >
    <div
      v-for="(color, index) in colors"
      :key="color"
      class="player"
      role="listitem"
      :aria-hidden="!active"
      :style="{
        color,
        '--join-delay': `${1100 + index * 220}ms`,
        '--join-tilt': `${index % 2 ? 12 : -12}deg`,
      }"
    >
      <svg viewBox="0 0 64 76" aria-hidden="true">
        <ellipse cx="32" cy="71" rx="19" ry="3" class="player-shadow" />
        <g class="meeple">
          <circle cx="32" cy="13" r="10" />
          <path
            d="M24 24h16l18 15-8 10-10-8 6 24H34l-2-15-2 15H18l6-24-10 8-8-10z"
          />
        </g>
      </svg>
      <span>P{{ index + 1 }}</span>
    </div>
  </div>
</template>

<style scoped>
.co-op-players {
  display: flex;
  justify-content: center;
  gap: 30px;
  margin-top: 36px;
}
.player {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
  opacity: 0;
  font-family: var(--slidev-code-font-family);
  font-size: 18px;
  font-weight: 700;
}
.player svg {
  width: 58px;
  height: 69px;
  overflow: visible;
}
.meeple {
  fill: currentColor;
  transform-origin: 32px 65px;
}
.player-shadow {
  fill: currentColor;
  opacity: 0.18;
}
.active .player {
  animation: player-join 650ms var(--join-delay) both;
}
@keyframes player-join {
  0% {
    opacity: 0;
    transform: translateY(-24px) scale(0.7) rotate(var(--join-tilt));
  }
  45% {
    opacity: 1;
    transform: translateY(3px) scale(1.06, 0.94) rotate(0);
  }
  70% {
    opacity: 1;
    transform: translateY(-4px) scale(0.98, 1.02);
  }
  100% {
    opacity: 1;
    transform: none;
  }
}
@media (prefers-reduced-motion: reduce) {
  .active .player {
    animation: none;
    opacity: 1;
  }
}
</style>
