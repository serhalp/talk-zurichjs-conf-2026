<script setup lang="ts">
import { onBeforeUnmount, ref, watch } from "vue";

const props = defineProps<{ active: boolean }>();
const level = ref(3);
let timers: ReturnType<typeof setTimeout>[] = [];

function reset() {
  timers.forEach(clearTimeout);
  timers = [];
}

watch(
  () => props.active,
  (active) => {
    reset();
    level.value = 3;
    if (active) {
      timers = [
        setTimeout(() => (level.value = 4), 500),
        setTimeout(() => (level.value = 5), 1300),
      ];
    }
  },
  { immediate: true },
);

onBeforeUnmount(reset);
</script>

<template>
  <LevelProgress v-if="active" :level="level" />
</template>
