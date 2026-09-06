<script setup lang="ts">
import { useIsSlideActive } from "@slidev/client";

const active = useIsSlideActive();
</script>

<template>
  <span class="nuxt-walk w-10 h-10" :class="{ arriving: active }">
    <img src="/nuxt.svg" alt="Nuxt" class="w-10 h-10 brightness-0 invert" />
  </span>
</template>

<style scoped>
.nuxt-walk {
  display: inline-block;
  position: relative;
  z-index: 1;
}
.arriving {
  animation: walk-in 2400ms 600ms linear both;
}
.arriving img {
  transform-origin: 50% 100%;
  animation: waddle 400ms 600ms ease-in-out 6;
}
@keyframes walk-in {
  from {
    opacity: 0;
    transform: translateX(180px);
  }
  15% {
    opacity: 1;
  }
  to {
    opacity: 1;
    transform: none;
  }
}
@keyframes waddle {
  0%,
  50%,
  100% {
    transform: none;
  }
  25% {
    transform: translateY(-3px) rotate(-17deg);
  }
  75% {
    transform: translateY(-3px) rotate(17deg);
  }
}
@media (prefers-reduced-motion: reduce) {
  .arriving,
  .arriving img {
    animation: none;
  }
}
</style>
