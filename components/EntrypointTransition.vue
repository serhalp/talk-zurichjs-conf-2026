<script setup lang="ts">
import { nextTick, onBeforeUnmount, ref, watch } from "vue";

const props = defineProps<{ active: boolean; path: string }>();
const container = ref<HTMLElement>();
const flyingLabel = ref<HTMLElement>();
const moving = ref(false);
const labelStyle = ref<Record<string, string>>({});
let animation: Animation | undefined;
let revision = 0;

function findPath() {
  if (!container.value) return;
  const walker = document.createTreeWalker(
    container.value,
    NodeFilter.SHOW_TEXT,
  );
  while (walker.nextNode()) {
    const node = walker.currentNode;
    const start = node.textContent?.indexOf(props.path) ?? -1;
    if (start < 0 || !node.parentElement?.closest("pre")) continue;
    const range = document.createRange();
    range.setStart(node, start);
    range.setEnd(node, start + props.path.length);
    return range.getBoundingClientRect();
  }
}

watch(
  () => props.active,
  async (active) => {
    const current = ++revision;
    animation?.cancel();
    moving.value = false;
    if (!active || matchMedia("(prefers-reduced-motion: reduce)").matches)
      return;
    const origin = findPath();
    if (!origin || !container.value) return;
    const scale =
      container.value.getBoundingClientRect().width /
      container.value.offsetWidth;
    const code = container.value.querySelector("code");
    const fontSize =
      parseFloat(getComputedStyle(code ?? container.value).fontSize) * scale;
    labelStyle.value = {
      left: `${origin.left}px`,
      top: `${origin.top}px`,
      fontSize: `${fontSize}px`,
    };
    moving.value = true;
    await nextTick();
    if (current !== revision) return;
    const title = container.value?.querySelector<HTMLElement>(
      ".slidev-code-block-title",
    );
    if (!title || !flyingLabel.value) {
      moving.value = false;
      return;
    }
    const target = title.getBoundingClientRect();
    animation = flyingLabel.value.animate(
      [
        {
          left: `${origin.left}px`,
          top: `${origin.top}px`,
          fontSize: `${fontSize}px`,
        },
        {
          left: `${target.left}px`,
          top: `${target.top}px`,
          fontSize: `${parseFloat(getComputedStyle(title).fontSize) * scale}px`,
        },
      ],
      {
        duration: 700,
        easing: "cubic-bezier(0.65, 0, 0.35, 1)",
        fill: "forwards",
      },
    );
    try {
      await animation.finished;
    } catch {
      return;
    }
    if (current === revision) moving.value = false;
  },
);

onBeforeUnmount(() => {
  revision++;
  animation?.cancel();
});
</script>

<template>
  <div ref="container">
    <div v-if="active" class="runtime" :class="{ moving }">
      <slot name="runtime" />
    </div>
    <slot v-else />
    <Teleport to="body">
      <span
        v-if="moving"
        ref="flyingLabel"
        class="flying-label"
        :style="labelStyle"
        >{{ path }}</span
      >
    </Teleport>
  </div>
</template>

<style scoped>
.runtime {
  transition: opacity 300ms ease;
}
.runtime.moving {
  opacity: 0;
}
.flying-label {
  position: fixed;
  z-index: 100;
  pointer-events: none;
  white-space: nowrap;
  color: #cbd5e1;
  font-family: var(--slidev-code-font-family);
  line-height: 1;
}
@media (prefers-reduced-motion: reduce) {
  .runtime {
    transition: none;
  }
}
</style>
