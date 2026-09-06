<script setup lang="ts">
import { useIsSlideActive } from "@slidev/client";

const active = useIsSlideActive();
</script>

<template>
  <img
    src="/nitro.svg"
    alt="Nitro"
    class="w-10 h-10"
    :class="{ arriving: active }"
  />
</template>

<style scoped>
.arriving {
  animation:
    fade-in 2600ms ease-out both,
    shake 130ms linear 20;
}
@keyframes fade-in {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
@keyframes shake {
  0%,
  100% {
    transform: none;
  }
  20% {
    transform: translate(-6px, 3px) rotate(-16deg);
  }
  40% {
    transform: translate(5px, -4px) rotate(13deg);
  }
  60% {
    transform: translate(-4px, -2px) rotate(-11deg);
  }
  80% {
    transform: translate(6px, 4px) rotate(17deg);
  }
}
@media (prefers-reduced-motion: reduce) {
  .arriving {
    animation: none;
  }
}
</style>
