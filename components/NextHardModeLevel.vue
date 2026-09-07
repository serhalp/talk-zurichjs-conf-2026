<script setup lang="ts">
import { useIsSlideActive } from "@slidev/client";
import { ref, watch } from "vue";

const props = defineProps<{ visible: boolean }>();
const active = useIsSlideActive();
const level = ref(6);
let timer: ReturnType<typeof setTimeout> | undefined;

watch(
  [active, () => props.visible],
  (_value, _previous, onCleanup) => {
    level.value = 6;
    onCleanup(() => clearTimeout(timer));
  },
  { immediate: true },
);

function afterEnter() {
  timer = setTimeout(() => {
    level.value = 7;
  }, 1000);
}
</script>

<template>
  <Transition name="badge-entry" appear @after-enter="afterEnter">
    <LevelProgress v-if="visible && active" :level="level" />
  </Transition>
</template>

<style scoped>
.badge-entry-enter-active {
  transition:
    opacity 400ms ease,
    transform 400ms ease;
}
.badge-entry-enter-from {
  opacity: 0;
  transform: translateY(8px);
}
@media (prefers-reduced-motion: reduce) {
  .badge-entry-enter-active {
    transition: none;
  }
}
</style>
