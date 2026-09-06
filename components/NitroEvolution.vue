<script setup lang="ts">
defineProps<{ evolved: boolean }>();
</script>

<template>
  <svg
    :viewBox="`0 0 868 ${evolved ? 132 : 172}`"
    role="img"
    :aria-label="
      evolved
        ? 'Vite builds TanStack Start with a separate Nitro v3 plugin containing the ZurichCloud preset.'
        : 'Nuxt includes Nitro v2, which contains its builder and the ZurichCloud preset.'
    "
    :class="{ evolved }"
  >
    <rect
      x="8"
      y="4"
      width="64"
      :height="evolved ? 120 : 160"
      class="version-tab"
    />
    <text
      x="40"
      :y="evolved ? 76 : 96"
      text-anchor="middle"
      class="version-label"
    >
      {{ evolved ? "v3" : "v2" }}
    </text>
    <rect
      x="88"
      y="4"
      width="616"
      :height="evolved ? 120 : 160"
      class="outer"
    />
    <g class="old-label">
      <image
        href="/nuxt.svg"
        x="104"
        y="10"
        width="32"
        height="32"
        class="mono"
      />
      <text x="149" y="36">Nuxt</text>
    </g>
    <g class="new-label">
      <image href="/vite.svg" x="104" y="10" width="32" height="32" />
      <text x="149" y="36">Vite</text>
    </g>

    <g class="nitro-frame">
      <rect x="0" y="0" height="108" class="nitro-background" />
      <image href="/nitro.svg" x="14" y="6" width="28" height="28" />
      <text :x="evolved ? 48 : 58" y="29">
        {{ evolved ? "Nitro Vite plugin" : "Nitro" }}
      </text>
    </g>

    <g class="builder">
      <rect x="120" y="92" width="212" height="56" />
      <text x="226" y="129" text-anchor="middle">builder</text>
    </g>
    <g class="tanstack">
      <rect x="104" y="92" width="238" height="56" />
      <image
        href="/tanstack.svg"
        x="116"
        y="105"
        width="30"
        height="30"
        class="mono"
      />
      <text x="159" y="128">TanStack Start</text>
    </g>

    <g :transform="evolved ? 'translate(0 -40)' : undefined">
      <text x="393" y="105" text-anchor="middle" class="server">server</text>
      <path d="M354 128H432m-7-5 7 5-7 5" />

      <rect x="452" y="92" width="232" height="56" />
      <image href="/zurich-cloud.svg" x="507" y="96" width="122" height="20" />
      <text x="568" y="140" text-anchor="middle">Nitro preset</text>

      <path d="M684 128H738m-7-5 7 5-7 5" />
      <text x="822" y="118" text-anchor="middle" class="function">
        ZurichCloud
      </text>
      <text x="822" y="148" text-anchor="middle" class="function">
        Functions
      </text>
    </g>
  </svg>
</template>

<style scoped>
svg {
  overflow: visible;
}
text {
  fill: #f8fafc;
  font-size: 24px;
}
rect {
  fill: #17202e;
  stroke: #64748b;
  stroke-width: 1.5;
  rx: 8px;
}
.outer {
  fill: #11151b;
}
.version-tab {
  fill: #292d34;
  stroke: #94a3b8;
}
.version-label {
  font-family: var(--slidev-code-font-family);
  font-size: 32px;
  font-weight: 700;
}
path {
  fill: none;
  stroke: #94a3b8;
  stroke-width: 1.5;
}
.mono {
  filter: brightness(0) invert(1);
}
.server {
  fill: #c4b5fd;
}
.function {
  fill: #67e8f9;
}
.nitro-frame {
  transform: translate(104px, 48px);
}
.nitro-background {
  width: 588px;
}
.new-label,
.tanstack {
  opacity: 0;
}
.evolved .nitro-frame {
  transform: translate(440px, 8px);
}
.evolved .tanstack {
  transform: translateY(-40px);
}
.evolved .nitro-background {
  width: 252px;
}
.evolved .old-label,
.evolved .builder {
  opacity: 0;
}
.evolved .new-label,
.evolved .tanstack {
  opacity: 1;
}
</style>
