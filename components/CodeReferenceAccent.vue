<script setup lang="ts">
import { nextTick, onBeforeUnmount, onMounted, ref, watch } from "vue";

const props = defineProps<{ active: boolean; text: string }>();
const container = ref<HTMLElement>();
let observer: MutationObserver | undefined;

function highlight() {
  container.value
    ?.querySelectorAll("span, .slidev-code-block-title div")
    .forEach((element) => {
      const text = element.textContent?.trim();
      element.classList.toggle(
        "code-reference-accent",
        props.active &&
          (text === props.text ||
            text === `"${props.text}"` ||
            text === `'${props.text}'`),
      );
    });
}

onMounted(() => {
  // Magic Move replaces tokens as the snippet changes.
  observer = new MutationObserver(highlight);
  observer.observe(container.value!, {
    childList: true,
    subtree: true,
    characterData: true,
  });
  highlight();
});
watch(
  () => [props.active, props.text],
  async () => {
    await nextTick();
    highlight();
  },
);
onBeforeUnmount(() => observer?.disconnect());
</script>

<template>
  <div ref="container"><slot /></div>
</template>

<style scoped>
:deep(.code-reference-accent) {
  color: #67e8f9 !important;
}
</style>
