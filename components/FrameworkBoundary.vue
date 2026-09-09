<script setup lang="ts">
defineProps<{ step: number; metadata?: boolean; settled?: boolean }>();

const connections = [
  {
    id: "developer-framework",
    d: "M660 44v23",
    step: 1,
    delay: 0,
    svelte: true,
  },
  {
    id: "developer-adapter",
    d: "M842 44v185",
    step: 1,
    delay: 350,
    svelte: true,
  },
  { id: "developer-cloud", d: "M35 44v286q0 12 12 12h70", step: 1, delay: 700 },
  { id: "developer-vite", d: "M485 44v111", step: 1, delay: 1050 },
  { id: "framework-vite", d: "M660 126v29", step: 2, delay: 0, svelte: true },
  {
    id: "adapter-framework",
    d: "M778 232V129",
    step: 3,
    delay: 0,
    svelte: true,
  },
  { id: "adapter-vite", d: "M660 232v-25", step: 3, delay: 350, svelte: true },
  { id: "adapter-cloud", d: "M660 288v29", step: 3, delay: 700, svelte: true },
  { id: "developer-tanstack", d: "M310 44v23", step: 4, delay: 250 },
  { id: "tanstack-vite", d: "M310 126v29", step: 4, delay: 600 },
  {
    id: "developer-plugin",
    d: "M70 44v204q0 12 12 12h65",
    step: 5,
    delay: 200,
  },
  { id: "plugin-vite", d: "M310 232v-25", step: 5, delay: 550 },
  { id: "plugin-cloud", d: "M310 288v29", step: 5, delay: 900 },
];
</script>

<template>
  <svg
    viewBox="0 0 868 364"
    role="img"
    :class="{ 'focus-plugins': step >= 4 && step < 7, settled }"
    aria-label="Both platform integrations connect to Vite and ZurichCloud. The adapter connects directly to its framework; a red broken arrow marks the unavailable framework-specific connection from the Vite plugin."
  >
    <defs>
      <marker
        id="boundary-arrow"
        viewBox="0 0 10 10"
        refX="9"
        refY="5"
        markerWidth="7"
        markerHeight="7"
        orient="auto-start-reverse"
      >
        <path d="m2 1 7 4-7 4" />
      </marker>
      <clipPath id="boundary-cat">
        <rect x="316" y="3" width="38" height="38" rx="7" />
      </clipPath>
    </defs>

    <g
      v-for="connection in connections"
      :key="connection.id"
      :class="{ 'svelte-side': connection.svelte }"
    >
      <g
        class="connection-stage"
        :class="{ shown: step >= connection.step }"
        :style="{ '--draw-delay': connection.delay + 'ms' }"
      >
        <path class="draw-arrow" :d="connection.d" pathLength="1" />
        <path
          class="arrow-head"
          :d="connection.d"
          marker-end="url(#boundary-arrow)"
        />
      </g>
    </g>

    <g class="blocked-connection reveal" :class="{ visible: step >= 6 && !metadata }">
      <path class="blocked-shaft" d="M190 232v-56" />
      <path class="blocked-shaft" d="M190 154v-25" />
      <path d="m185 136 5-7 5 7" />
      <path class="blocked-cross" d="m184 158 12 12m0-12-12 12" />
    </g>

    <g class="metadata-connection reveal" :class="{ visible: metadata }">
      <path d="M190 232V129m-5 7 5-7 5 7" />
      <rect x="83" y="151" width="147" height="59" rx="8" />
      <text x="156" y="175" text-anchor="middle">Deployment<tspan x="156" dy="23">metadata?</tspan></text>
    </g>

    <rect x="8" y="0" width="852" height="44" rx="9" />
    <image
      href="/patak-cat.png"
      x="316"
      y="3"
      width="38"
      height="38"
      preserveAspectRatio="xMidYMid slice"
      clip-path="url(#boundary-cat)"
    />
    <text x="372" y="31">Web developer</text>

    <g class="reveal" :class="{ visible: step >= 4 }">
      <rect x="150" y="70" width="320" height="56" rx="9" />
      <image href="/tanstack.svg" x="168" y="80" width="36" height="36" />
      <text x="222" y="107">TanStack Start</text>
    </g>

    <g class="svelte-side">
      <rect x="500" y="70" width="300" height="56" rx="9" />
      <image
        href="/svelte.svg"
        x="518"
        y="80"
        width="36"
        height="36"
        class="mono"
      />
      <text x="572" y="107">SvelteKit</text>
    </g>

    <rect x="240" y="158" width="500" height="46" rx="9" />
    <image href="/vite.svg" x="428" y="165" width="32" height="32" />
    <text x="478" y="190">Vite</text>

    <g class="reveal" :class="{ visible: step >= 5 }">
      <rect x="150" y="232" width="320" height="56" rx="9" />
      <g transform="translate(168 245) scale(1.25)">
        <path d="M1 1h22v22z" fill="#fff" />
        <path d="M1 1v22h22z" fill="#38bdf8" />
      </g>
      <image href="/vite.svg" x="208" y="245" width="30" height="30" />
      <text x="254" y="256">
        ZurichCloud
        <tspan x="254" dy="25">Vite plugin</tspan>
      </text>
    </g>

    <g class="svelte-side">
      <rect x="500" y="232" width="360" height="56" rx="9" />
      <g transform="translate(518 245) scale(1.25)">
        <path d="M1 1h22v22z" fill="#fff" />
        <path d="M1 1v22h22z" fill="#38bdf8" />
      </g>
      <image
        href="/svelte.svg"
        x="558"
        y="245"
        width="30"
        height="30"
        class="mono"
      />
      <text x="604" y="256">
        ZurichCloud
        <tspan x="604" dy="25">SvelteKit adapter</tspan>
      </text>
    </g>

    <rect x="120" y="320" width="700" height="44" rx="9" />
    <g transform="translate(366 327) scale(1.25)">
      <path d="M1 1h22v22z" fill="#fff" />
      <path d="M1 1v22h22z" fill="#38bdf8" />
    </g>
    <text x="414" y="351">ZurichCloud</text>
  </svg>
</template>

<style scoped>
svg {
  display: block;
  width: 100%;
}
rect {
  fill: #17202e;
  stroke: #64748b;
  stroke-width: 1.3;
}
text {
  fill: #f8fafc;
  font-family: inherit;
  font-size: 25px;
}
.mono {
  filter: brightness(0) invert(1);
}
.draw-arrow,
marker path {
  fill: none;
  stroke: #bef264;
  stroke-width: 1.8;
  stroke-linecap: round;
  stroke-linejoin: round;
}
marker path {
  stroke-width: 1.3;
}
.blocked-connection {
  fill: none;
  stroke: #f87171;
  stroke-width: 2;
  stroke-linecap: round;
  stroke-linejoin: round;
}
.blocked-shaft {
  stroke-dasharray: 5 4;
}
.blocked-cross {
  stroke-width: 2.5;
}
.metadata-connection path { fill: none; stroke: #67e8f9; stroke-width: 2; stroke-dasharray: 5 4; }
.metadata-connection rect { fill: #142c34; stroke: #67e8f9; }
.metadata-connection text { fill: #a5f3fc; font-size: 21px; }
.settled .shown .draw-arrow { animation: none; stroke-dashoffset: 0; }
.settled .shown .arrow-head { animation: none; opacity: 1; }

.svelte-side {
  transition: opacity 500ms ease;
}
.focus-plugins .svelte-side {
  opacity: 0.2;
}
.reveal {
  opacity: 0;
  visibility: hidden;
  transition:
    opacity 450ms ease,
    visibility 450ms;
}
.reveal.visible {
  opacity: 1;
  visibility: visible;
}
.connection-stage {
  visibility: hidden;
}
.connection-stage.shown {
  visibility: visible;
}
.draw-arrow {
  stroke-dasharray: 1;
  stroke-dashoffset: 1;
}
.shown .draw-arrow {
  animation: draw-connection 650ms ease var(--draw-delay) both;
}
.arrow-head {
  fill: none;
  stroke: none;
  opacity: 0;
}
.shown .arrow-head {
  animation: show-arrowhead 120ms ease calc(var(--draw-delay) + 600ms) both;
}
@keyframes draw-connection {
  to {
    stroke-dashoffset: 0;
  }
}
@keyframes show-arrowhead {
  to {
    opacity: 1;
  }
}
@media (prefers-reduced-motion: reduce) {
  .svelte-side,
  .reveal {
    transition: none;
  }
  .shown .draw-arrow {
    animation: none;
    stroke-dashoffset: 0;
  }
  .shown .arrow-head {
    animation: none;
    opacity: 1;
  }
}
</style>
