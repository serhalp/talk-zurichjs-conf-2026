<script setup lang="ts">
defineProps<{ routed: boolean }>();
</script>

<template>
  <svg
    viewBox="0 0 868 204"
    role="img"
    aria-label="Requests to about and API cart must be routed to different request handlers"
  >
    <image href="/patak-cat.png" x="0" y="60" width="94" height="94" />
    <g
      v-for="(route, index) in [
        { url: '/about', name: 'SSR function' },
        { url: '/api/cart', name: 'API function' },
      ]"
      :key="route.url"
      :transform="`translate(0, ${index * 100})`"
    >
      <rect x="122" y="24" width="350" height="68" rx="8" class="box" />
      <text x="138" y="52" class="host">https://hello.zurich.cloud</text>
      <text x="138" y="80" class="path">{{ route.url }}</text>
      <path v-if="routed" d="M484 58h87m-8-7 8 7-8 7" class="arrow" />
      <text v-else x="527" y="70" class="question" text-anchor="middle">?</text>
      <rect x="590" y="24" width="270" height="68" rx="8" class="box" />
      <text x="725" y="66" text-anchor="middle" class="function">
        {{ route.name }}
      </text>
    </g>
  </svg>
</template>

<style scoped>
svg {
  width: 100%;
}
text {
  font-family: inherit;
  fill: #f8fafc;
}
.host {
  font-size: 24px;
  fill: #cbd5e1;
}
.path {
  font-family: var(--slidev-code-font-family);
  font-size: 24px;
}
.function {
  font-size: 28px;
  fill: #67e8f9;
}
.question {
  font-size: 38px;
  fill: #bef264;
}
.box {
  fill: #17202e;
  stroke: #94a3b8;
  stroke-width: 1.5;
}
.arrow {
  fill: none;
  stroke: #94a3b8;
  stroke-width: 1.5;
  stroke-linecap: round;
  stroke-linejoin: round;
}
</style>
