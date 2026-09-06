<script setup lang="ts">
import { useIsSlideActive } from "@slidev/client";

const active = useIsSlideActive();
</script>

<template>
  <img
    src="/astro.svg"
    alt="Astro"
    class="astro-rocket w-10 h-10 brightness-0 invert"
    :class="{ 'is-landing': active }"
  />
</template>

<style scoped>
.astro-rocket {
  position: relative;
  z-index: 1;
  transform-origin: 50% 90%;
}
.is-landing {
  animation: touchdown 2200ms 150ms both;
}
@keyframes touchdown {
  0% {
    transform: translateY(520px) rotate(-8deg);
    animation-timing-function: cubic-bezier(0.4, 0.1, 0.3, 1);
  }
  65% {
    transform: translateY(0) scale(1.12, 0.88) rotate(2deg);
    animation-timing-function: ease-out;
  }
  80% {
    transform: translateY(-9px) scale(0.97, 1.03) rotate(-2deg);
    animation-timing-function: ease-in;
  }
  92% {
    transform: translateY(0) scale(1.03, 0.97);
  }
  100% {
    transform: none;
  }
}
@media (prefers-reduced-motion: reduce) {
  .is-landing {
    animation: none;
  }
}
</style>
