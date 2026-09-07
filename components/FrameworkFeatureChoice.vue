<script setup lang="ts">
defineProps<{ step: number }>();

const features = [
  "Image CDN configuration",
  "Redirects and rewrites",
  "Static response headers",
];
</script>

<template>
  <svg
    viewBox="0 0 868 278"
    role="img"
    aria-label="Image CDN configuration, redirects and rewrites, and static response headers can be left to users to configure on their platform. Skew protection still needs framework and platform coordination."
  >
    <g class="platform-area" :class="{ shown: step >= 1, dimmed: step >= 4 }">
      <rect
        x="420"
        y="0"
        width="448"
        height="220"
        rx="12"
        class="platform-box"
      />
      <text x="442" y="34" class="heading">Configure on the platform</text>
    </g>
    <g
      v-for="(feature, index) in features"
      :key="feature"
      class="feature"
      :class="{ moved: step > index, dimmed: step >= 4 }"
      :style="{
        transform: `translate(${step > index ? 438 : 0}px, ${60 + index * 54}px)`,
      }"
    >
      <rect width="410" height="44" rx="7" />
      <text x="16" y="30">{{ feature }}</text>
    </g>
    <g
      class="skew-feature"
      :class="{ highlighted: step >= 4 }"
      transform="translate(0 228)"
    >
      <rect width="410" height="44" rx="7" />
      <text x="16" y="30">Skew protection</text>
      <text
        x="438"
        y="30"
        class="coordination-label"
        :class="{ shown: step >= 4 }"
      >
        This needs coordination.
      </text>
    </g>
  </svg>
</template>

<style scoped>
svg {
  display: block;
  width: 100%;
  overflow: visible;
}
text {
  font-family: inherit;
  font-size: 25px;
  fill: #f8fafc;
}
rect {
  fill: #17202e;
  stroke: #64748b;
  stroke-width: 1.3;
  transition:
    fill 400ms,
    stroke 400ms;
}
.platform-box {
  fill: #131a23;
  stroke-dasharray: 5 5;
}
.heading {
  fill: #cbd5e1;
}
.platform-area {
  opacity: 0;
  transition: opacity 400ms;
}
.platform-area.shown {
  opacity: 1;
}
.feature {
  transition:
    transform 750ms cubic-bezier(0.4, 0, 0.2, 1),
    opacity 400ms;
}
.feature.moved rect {
  stroke: #94a3b8;
}
.dimmed,
.platform-area.dimmed {
  opacity: 0.25;
}
.skew-feature.highlighted rect {
  fill: #153039;
  stroke: #67e8f9;
}
.coordination-label {
  opacity: 0;
  fill: #67e8f9;
  transition: opacity 400ms;
}
.coordination-label.shown {
  opacity: 1;
}
@media (prefers-reduced-motion: reduce) {
  * {
    transition: none !important;
  }
}
</style>
