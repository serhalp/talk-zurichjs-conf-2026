<script setup lang="ts">
withDefaults(
  defineProps<{
    showVite?: boolean;
    focus?: "vite" | "framework";
  }>(),
  { showVite: true },
);
</script>

<template>
  <div class="integration-surfaces" :class="focus && `focus-${focus}`">
    <div class="framework-surface">
      <h2>The framework's own API</h2>
      <div class="surface-frameworks">
        <span><img src="/astro.svg" alt="" class="surface-mono" />Astro</span>
        <span
          ><img src="/svelte.svg" alt="" class="surface-mono" />SvelteKit</span
        >
        <span><img src="/nuxt.svg" alt="" class="surface-mono" />Nuxt</span>
      </div>
      <p>We write an adapter for that framework.</p>
    </div>
    <div class="vite-surface" :class="{ 'surface-hidden': !showVite }">
      <h2><img src="/vite.svg" alt="" />Vite</h2>
      <div class="surface-frameworks">
        <span
          ><img src="/reactrouter.svg" alt="" class="surface-mono" /><span
            class="surface-name"
            >React<br />Router</span
          ></span
        >
        <span
          ><img src="/tanstack.svg" alt="" /><span class="surface-name"
            >TanStack<br />Start</span
          ></span
        >
        <span
          ><img src="/fetchable/solid.svg" alt="" /><span class="surface-name"
            >SolidStart</span
          ></span
        >
      </div>
      <p>We write a Vite plugin for that framework.</p>
    </div>
  </div>
</template>

<style scoped>
.integration-surfaces {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 26px;
  margin: 34px 0 26px;
}
.integration-surfaces > div {
  border: 1px solid #64748b;
  border-radius: 12px;
  padding: 24px;
  background: #17202e;
  transition:
    opacity 500ms,
    border-color 500ms;
}
.integration-surfaces h2 {
  display: flex;
  align-items: center;
  gap: 12px;
  margin: 0 0 28px;
  font-size: 27px;
}
.integration-surfaces h2 img {
  width: 32px;
  height: 32px;
}
.surface-frameworks {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  align-items: start;
  gap: 12px;
  min-height: 104px;
}
.surface-frameworks > span {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
  font-size: 22px;
  white-space: nowrap;
}
.surface-name {
  text-align: center;
  line-height: 1.25;
}
.surface-frameworks img {
  width: 38px;
  height: 38px;
  object-fit: contain;
}
.surface-frameworks .surface-mono {
  filter: brightness(0) invert(1);
}
.integration-surfaces p {
  margin: 24px 0 0;
  font-size: 24px;
  line-height: 1.4;
}
.focus-vite .framework-surface,
.focus-framework .vite-surface {
  opacity: 0.3;
}
.focus-vite .vite-surface,
.focus-framework .framework-surface {
  border-color: #bef264;
}
.integration-surfaces .surface-hidden {
  opacity: 0;
}
@media (prefers-reduced-motion: reduce) {
  .integration-surfaces > div {
    transition: none;
  }
}
</style>
