<script setup lang="ts">
import { useIsSlideActive } from "@slidev/client";
import { ref, watch } from "vue";

const active = useIsSlideActive();
const corrected = ref(false);

watch(
  active,
  (isActive, _previous, onCleanup) => {
    corrected.value = false;
    if (!isActive) return;
    const timer = setTimeout(() => {
      corrected.value = true;
    }, 5000);
    onCleanup(() => clearTimeout(timer));
  },
  { immediate: true },
);
</script>

<template>
  <span class="dogfood-word"
    >Dogf<span class="correction-target"
      >ooded<template v-if="corrected">
        <svg
          class="cross-out"
          viewBox="0 0 140 24"
          preserveAspectRatio="none"
          aria-hidden="true"
        >
          <path pathLength="1" d="M3 17Q42 10 78 12T137 5M132 17Q83 11 9 8" />
        </svg>
        <svg
          class="scribbled-correction"
          viewBox="0 0 90 40"
          aria-hidden="true"
        >
          <path pathLength="1" d="M9 25Q27 22 23 16Q18 10 10 20Q3 34 26 29" />
          <path
            pathLength="1"
            d="M48 18Q33 11 31 26Q30 34 39 30Q51 23 54 3L47 31"
          />
          <path
            pathLength="1"
            d="M64 12Q66 2 78 6Q89 13 75 20L72 25M72 32l.5 1"
          />
        </svg> </template></span
  ></span>
</template>

<style scoped>
.dogfood-word {
  white-space: nowrap;
}
.correction-target {
  position: relative;
}
.cross-out {
  position: absolute;
  left: -3px;
  top: 34%;
  width: calc(100% + 6px);
  height: 20px;
  overflow: visible;
}
.cross-out path,
.scribbled-correction path {
  fill: none;
  stroke: currentColor;
  stroke-width: 2.5;
  stroke-linecap: round;
  stroke-linejoin: round;
  stroke-dasharray: 1;
  stroke-dashoffset: 1;
}
.cross-out path {
  color: #e2e8f0;
  animation: ink-in 500ms ease-out forwards;
}
.scribbled-correction {
  position: absolute;
  left: 20%;
  top: 94%;
  width: 64px;
  height: 29px;
  overflow: visible;
  transform: rotate(-8deg);
  color: #bef264;
}
.scribbled-correction path {
  animation: ink-in 300ms 600ms ease-out forwards;
}
.scribbled-correction path:nth-child(2) {
  animation-delay: 850ms;
}
.scribbled-correction path:nth-child(3) {
  animation-delay: 1100ms;
}
@keyframes ink-in {
  to {
    stroke-dashoffset: 0;
  }
}
@media (prefers-reduced-motion: reduce) {
  .cross-out path,
  .scribbled-correction path {
    animation: none;
    stroke-dashoffset: 0;
  }
}
</style>
