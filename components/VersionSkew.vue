<script setup lang="ts">
defineProps<{ step: number }>();
</script>

<template>
  <svg
    viewBox="0 0 868 260"
    role="img"
    aria-label="An open browser tab still runs deployment A after deployment B goes live; version skew protection keeps its framework requests on deployment A"
  >
    <image href="/patak-cat.png" x="0" y="70" width="85" height="85" />
    <rect x="108" y="22" width="300" height="170" rx="12" class="box" />
    <path d="M108 64h300" class="arrow" />
    <text x="130" y="51" class="small">https://hello.zurich.cloud/about</text>
    <text x="258" y="105" text-anchor="middle">An open tab</text>
    <text x="258" y="150" text-anchor="middle" class="version">
      Deployment A
    </text>
    <rect x="598" y="22" width="264" height="170" rx="12" class="box" />
    <text x="730" y="65" text-anchor="middle">Server</text>
    <text
      x="730"
      y="105"
      text-anchor="middle"
      :class="step === 1 ? 'mismatch' : 'version'"
    >
      Deployment {{ step === 1 ? "B" : "A" }}
    </text>
    <text v-if="step >= 1" x="730" y="150" text-anchor="middle" class="small">
      {{ step === 1 ? "New version is live" : "A is retained" }}
    </text>
    <path d="M425 108h153m-8-7 8 7-8 7" class="arrow" />
    <text x="501" y="87" text-anchor="middle" class="small">Request</text>
    <g v-if="step >= 2">
      <rect x="424" y="131" width="153" height="38" rx="5" class="tag" />
      <text x="500" y="158" text-anchor="middle" class="small">version: A</text>
    </g>
  </svg>
</template>

<style scoped>
svg {
  width: 100%;
}
text {
  fill: #f8fafc;
  font-size: 28px;
  font-family: inherit;
}
.small {
  font-size: 24px;
}
.version {
  fill: #bef264;
}
.mismatch {
  fill: #fdba74;
}
.box {
  fill: #17202e;
  stroke: #94a3b8;
  stroke-width: 1.5;
}
.arrow {
  stroke: #94a3b8;
  stroke-width: 1.5;
  fill: none;
  stroke-linecap: round;
}
.tag {
  fill: #202b18;
  stroke: #bef264;
}
</style>
