<script setup lang="ts">
import { onBeforeUnmount, onMounted, ref } from "vue";

const props = defineProps<{ token: string; enabled: boolean }>();
const root = ref<HTMLElement>();
let observer: MutationObserver;

function markTokens() {
  root.value?.querySelectorAll("span").forEach((span) => {
    span.toggleAttribute(
      "data-token-accent",
      !span.children.length && span.textContent?.trim() === props.token,
    );
  });
}

onMounted(() => {
  markTokens();
  // Magic Move replaces tokens as the code changes.
  observer = new MutationObserver(markTokens);
  observer.observe(root.value!, {
    childList: true,
    subtree: true,
    characterData: true,
  });
});
onBeforeUnmount(() => observer?.disconnect());
</script>

<template>
  <div ref="root" :class="{ 'accent-enabled': enabled }"><slot /></div>
</template>

<style scoped>
.accent-enabled :deep([data-token-accent]) {
  color: #c4b5fd !important;
  text-decoration: underline;
  text-decoration-color: #c4b5fd;
  text-decoration-thickness: 2px;
  text-underline-offset: 5px;
}
</style>
