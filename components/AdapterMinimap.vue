<script setup lang="ts">
defineProps<{ highlight: boolean; delegated: boolean; astro: boolean }>();

const blocks = [
  {
    id: "framework",
    y: 42,
    rows: 5,
    label: ["Build server + manifest"],
    destinationY: 42,
    shared: false,
  },
  {
    id: "output",
    y: 80,
    rows: 13,
    label: ["Copy static assets", "+ prerendered pages"],
    destinationY: 106,
    shared: true,
  },
  {
    id: "framework-routing",
    y: 158,
    rows: 4,
    label: ["Resolve SvelteKit routes"],
    destinationY: 80,
    shared: false,
  },
  {
    id: "functions",
    y: 192,
    rows: 13,
    label: ["Generate + package", "Functions / Edge Functions"],
    destinationY: 184,
    shared: true,
  },
  {
    id: "routing",
    y: 271,
    rows: 10,
    label: ["Emit platform redirects", "+ response headers"],
    destinationY: 262,
    shared: true,
  },
  {
    id: "runtime",
    y: 335,
    rows: 3,
    label: ["Initialize SvelteKit’s server"],
    destinationY: 112,
    shared: false,
  },
];

// Decorative tokens suggest code density; they are not invented API examples.
const lines = (rows: number) =>
  Array.from({ length: rows }, (_, row) => {
    const indent = [0, 12, 24, 24, 36, 12, 24, 0][row % 8];
    return {
      indent,
      tokens: Array.from({ length: 3 + (row % 4) }, (_, token) => ({
        x: token * 28,
        width: 12 + ((row * 7 + token * 11) % 15),
        color: ["#c4b5fd", "#94a3b8", "#a3be8c", "#d6ae7b"][(row + token) % 4],
      })),
    };
  });

const sectionHeight = (rows: number) => (rows - 1) * 5.4 + 10;
</script>

<template>
  <svg
    viewBox="0 0 868 380"
    role="img"
    :class="{ highlight, delegated, astro }"
    aria-label="Most deployment code moves into the ZurichCloud Vite plugin. SvelteKit and Astro adapters retain framework-specific code and delegate to the same plugin."
  >
    <rect
      class="source-frame"
      x="20"
      y="26"
      width="266"
      :height="delegated ? 152 : 332"
      rx="8"
    />
    <g class="destination">
      <image
        href="/zurich-cloud-symbol.svg"
        x="560"
        y="38"
        width="30"
        height="30"
      />
      <image href="/vite.svg" x="600" y="38" width="30" height="30" />
      <text x="644" y="48">ZurichCloud</text>
      <text x="644" y="77">Vite plugin</text>
      <rect
        class="target-frame"
        x="560"
        y="92"
        width="266"
        height="226"
        rx="8"
      />
    </g>

    <g
      v-for="block in blocks"
      :key="block.id"
      class="code-section"
      :class="{ 'shared-blocks': block.shared, retained: !block.shared }"
      :style="{
        transform: delegated
          ? `translate(${block.shared ? 540 : 0}px, ${block.destinationY - block.y}px)`
          : 'translate(0, 0)',
      }"
    >
      <rect
        class="section-boundary"
        x="26"
        :y="block.y - 6"
        width="254"
        :height="sectionHeight(block.rows)"
        rx="4"
      />
      <g
        v-for="(line, row) in lines(block.rows)"
        :key="row"
        :transform="`translate(${38 + line.indent}, ${block.y + row * 5.4})`"
      >
        <rect
          v-for="(token, index) in line.tokens"
          :key="index"
          :x="token.x"
          :width="token.width"
          height="2.8"
          :fill="token.color"
        />
      </g>
    </g>

    <g class="annotations">
      <g
        v-for="block in blocks"
        :key="block.id"
        :class="{ 'shared-label': block.shared }"
      >
        <path
          :d="`M292 ${block.y - 6}h8v${sectionHeight(block.rows)}h-8 M300 ${block.y - 6 + sectionHeight(block.rows) / 2}h26`"
        />
        <text
          x="348"
          :y="
            block.y -
            6 +
            sectionHeight(block.rows) / 2 +
            (block.label.length === 1 ? 8 : -5)
          "
        >
          <tspan
            v-for="(line, index) in block.label"
            :key="line"
            x="348"
            :dy="index ? 26 : 0"
          >
            {{ line }}
          </tspan>
        </text>
      </g>
    </g>

    <g class="handoff">
      <rect
        x="36"
        y="142"
        width="234"
        height="24"
        rx="4"
        class="handoff-line"
      />
      <text x="47" y="160" class="handoff-text">Register Vite plugin</text>
      <path d="M290 154h254m-8-6 8 6-8 6" />
      <text x="355" y="138">Delegate</text>
      <text x="20" y="218" class="svelte-caption">
        SvelteKit knowledge stays.
      </text>
      <text x="560" y="353">One implementation.</text>
    </g>

    <g class="astro-adapter">
      <image
        href="/zurich-cloud-symbol.svg"
        x="20"
        y="188"
        width="28"
        height="28"
      />
      <image
        href="/astro.svg"
        x="58"
        y="188"
        width="28"
        height="28"
        class="astro-logo"
      />
      <text x="96" y="209" class="astro-title">ZurichCloud Astro adapter</text>
      <rect
        class="target-frame"
        x="20"
        y="228"
        width="266"
        height="130"
        rx="8"
      />
      <g
        v-for="(line, row) in lines(12)"
        :key="row"
        :transform="`translate(${38 + line.indent}, ${242 + row * 5.4})`"
      >
        <rect
          v-for="(token, index) in line.tokens"
          :key="index"
          :x="token.x"
          :width="token.width"
          height="2.8"
          :fill="token.color"
        />
      </g>
      <rect
        x="36"
        y="320"
        width="234"
        height="24"
        rx="4"
        class="handoff-line"
      />
      <text x="47" y="338" class="handoff-text">Register Vite plugin</text>
      <path class="astro-arrow" d="M290 300h254m-8-6 8 6-8 6" />
    </g>
  </svg>
</template>

<style scoped>
svg {
  display: block;
  width: 100%;
}
text {
  font-family: inherit;
  font-size: 24px;
  fill: #f8fafc;
}
.source-frame,
.target-frame {
  fill: #141c28;
  stroke: #64748b;
}
.source-frame {
  transition: height 1500ms ease-in-out;
}
.shared-blocks,
.retained {
  transition:
    transform 1500ms ease-in-out,
    opacity 450ms;
}
.section-boundary {
  fill: #94a3b8;
  fill-opacity: 0.035;
  stroke: #64748b;
  stroke-opacity: 0.55;
  transition:
    fill-opacity 450ms,
    stroke-opacity 450ms;
}
.highlight .shared-blocks .section-boundary {
  fill: #67e8f9;
  stroke: #67e8f9;
  fill-opacity: 0.07;
  stroke-opacity: 0.8;
}
.highlight:not(.delegated) .retained {
  opacity: 0.35;
}
.annotations {
  transition: opacity 300ms;
}
.annotations path,
.handoff path {
  fill: none;
  stroke: #94a3b8;
  stroke-width: 1.5;
}
.astro-arrow {
  fill: none;
  stroke: #94a3b8;
  stroke-width: 1.5;
}
.astro-adapter {
  opacity: 0;
  transform: translateY(12px);
  transition:
    opacity 650ms ease,
    transform 650ms ease;
}
.astro .astro-adapter {
  opacity: 1;
  transform: translateY(0);
}
.svelte-caption {
  transition: opacity 250ms;
}
.astro .svelte-caption {
  opacity: 0;
}
.astro-logo {
  filter: brightness(0) invert(1);
}
.astro-title {
  font-size: 22px;
}
.highlight .shared-label text {
  fill: #67e8f9;
}
.destination,
.handoff {
  opacity: 0;
  transition: opacity 350ms;
}
.delegated .annotations {
  opacity: 0;
}
.delegated .destination {
  opacity: 1;
  transition-delay: 400ms;
}
.delegated .handoff {
  opacity: 1;
  transition-delay: 1500ms;
}
.handoff-line {
  fill: #17333c;
  stroke: #67e8f9;
}
.handoff-text {
  font-size: 18px;
  fill: #67e8f9;
}
@media (prefers-reduced-motion: reduce) {
  * {
    transition: none !important;
  }
}
</style>
