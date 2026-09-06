<script setup lang="ts">
import { useIsSlideActive } from "@slidev/client";
import { ref, watch } from "vue";

const active = useIsSlideActive();
const props = defineProps<{ celebrate: boolean }>();
const level = ref(5);
const congratulated = ref(false);

watch(
  [active, () => props.celebrate],
  ([isActive, celebrate], _previous, onCleanup) => {
    level.value = 5;
    congratulated.value = false;
    if (!isActive || !celebrate) return;

    // Finish the fade and move, then pause half a second before leveling up.
    const timer = setTimeout(() => {
      level.value = 6;
    }, 1850);
    const bubbleTimer = setTimeout(() => {
      congratulated.value = true;
    }, 3950);
    onCleanup(() => {
      clearTimeout(timer);
      clearTimeout(bubbleTimer);
    });
  },
  { immediate: true },
);
</script>

<template>
  <div class="frontend-cloud-achievement" :class="{ centered: celebrate }">
    <LevelProgress :level="level" class="frontend-cloud-level" />
    <slot />
    <Transition name="congratulations">
      <div v-if="congratulated" class="congratulations-bubble">
        Congratulations, you now employ a
        <span class="whitespace-nowrap">full-time</span> frameworks team.
      </div>
    </Transition>
  </div>
</template>

<style scoped>
.frontend-cloud-achievement {
  position: absolute;
  z-index: 5;
  left: calc(100% - 56px);
  top: 12px;
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  gap: 8px;
  width: max-content;
  transform: translateX(-100%);
  transition:
    left 900ms 450ms ease,
    top 900ms 450ms ease,
    transform 900ms 450ms cubic-bezier(0.22, 1, 0.36, 1);
}
.centered {
  left: 50%;
  top: 55%;
  transform: translate(-50%, -50%) scale(1.35);
}
.frontend-cloud-level :deep(.level-up-label) {
  top: -28px;
  right: 12px;
}
.congratulations-bubble {
  position: absolute;
  top: calc(100% + 24px);
  left: 50%;
  width: 490px;
  padding: 16px 24px;
  transform: translateX(-50%);
  border: 2px solid #94a3b8;
  border-radius: 28px;
  background: #17202e;
  color: #f8fafc;
  font-size: 24px;
  line-height: 1.3;
  text-align: center;
}
.congratulations-enter-active {
  transition:
    opacity 350ms ease,
    translate 350ms ease;
}
.congratulations-enter-from {
  opacity: 0;
  translate: 0 8px;
}
@media (prefers-reduced-motion: reduce) {
  .congratulations-enter-active {
    transition: none;
  }
  .frontend-cloud-achievement {
    transition: none;
  }
}
</style>
