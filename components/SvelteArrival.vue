<script setup lang="ts">
import { useIsSlideActive } from "@slidev/client";

const active = useIsSlideActive();
</script>

<template>
  <img
    src="/svelte.svg"
    alt="SvelteKit"
    class="w-10 h-10 brightness-0 invert"
    :class="{ 'is-arriving': active }"
  />
</template>

<style scoped>
.is-arriving {
  animation: spin-in 1700ms 150ms both;
}
@keyframes spin-in {
  0% {
    transform: translateX(1000px) rotate(540deg);
    animation-timing-function: cubic-bezier(0.16, 0.8, 0.3, 1);
  }
  80% {
    transform: translateX(-7px) rotate(-12deg);
    animation-timing-function: ease-out;
  }
  100% {
    transform: none;
  }
}
@media (prefers-reduced-motion: reduce) {
  .is-arriving {
    animation: none;
  }
}
</style>
