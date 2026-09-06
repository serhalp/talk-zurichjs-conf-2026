<script setup lang="ts">
defineProps<{ step: number }>();
</script>

<template>
  <div class="choice-stage">
    <Transition name="clear">
      <div v-if="step < 2" class="comparison"><slot name="comparison" /></div>
    </Transition>
    <template v-if="step >= 2">
      <div class="install-line">
        <em>Users</em> install the Nitro Vite plugin:
      </div>
      <div class="examples">
        <div class="nitro-example"><slot name="nitro" /></div>
        <div v-if="step >= 3" class="alternative">
          <div class="alternative-label">
            Users can also choose alternative deployment plugins:
          </div>
          <slot name="alternative" />
        </div>
      </div>
    </template>
  </div>
</template>

<style scoped>
.choice-stage {
  position: relative;
}
.comparison {
  position: absolute;
  inset: 0 0 auto;
}
.clear-leave-active {
  transition:
    opacity 850ms ease,
    transform 850ms ease;
}
.clear-leave-to {
  opacity: 0;
  transform: translateY(-12px);
}
.install-line {
  position: absolute;
  top: 0;
  line-height: 1.25;
  animation: rise 1100ms cubic-bezier(0.22, 1, 0.36, 1) both;
}
.examples {
  padding-top: 36px;
}
.nitro-example {
  animation: reveal 450ms 1100ms ease-out both;
}
.alternative {
  margin-top: 10px;
  animation: reveal 350ms ease-out both;
}
.alternative-label {
  margin-bottom: 8px;
  line-height: 1.25;
}
.examples :deep(pre),
.examples :deep(code) {
  line-height: 1.05 !important;
}
.examples :deep(pre),
.examples :deep(.slidev-code-block-title) {
  padding: 4px 8px !important;
}
@keyframes rise {
  0% {
    opacity: 0;
    transform: translateY(354px);
  }
  20% {
    opacity: 1;
  }
  100% {
    opacity: 1;
    transform: none;
  }
}
@keyframes reveal {
  from {
    opacity: 0;
    transform: translateY(8px);
  }
  to {
    opacity: 1;
    transform: none;
  }
}
@media (prefers-reduced-motion: reduce) {
  .clear-leave-active {
    transition: none;
  }
  .install-line,
  .nitro-example,
  .alternative {
    animation: none;
  }
}
</style>
