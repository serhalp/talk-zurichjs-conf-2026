<script setup lang="ts">
defineProps<{ step: number }>();

const frameworks = [
  {
    name: "Astro",
    logo: "/astro.svg",
    integration: "Astro adapter",
    shared: false,
  },
  {
    name: "SvelteKit",
    logo: "/svelte.svg",
    integration: "SvelteKit adapter",
    shared: false,
  },
  {
    name: "React Router",
    logo: "/reactrouter.svg",
    integration: "RR Vite plugin",
    shared: true,
  },
  {
    name: "Nuxt",
    logo: "/nitro.svg",
    integration: "Nitro preset",
    shared: true,
  },
];
</script>

<template>
  <svg
    viewBox="0 0 868 442"
    role="img"
    aria-label="Server deployment: Astro and SvelteKit build with Vite and expose separate adapter APIs. React Router's platform plugin participates in Vite. Nuxt delegates the server build and platform preset to Nitro."
    class="comparison"
  >
    <g
      v-for="(framework, index) in frameworks"
      :key="framework.name"
      class="row"
      :class="{ visible: step >= index }"
      :transform="`translate(0 ${8 + index * 100})`"
    >
      <template v-if="index === 2">
        <text x="0" y="53">React</text>
        <text x="0" y="81">Router</text>
      </template>
      <text v-else x="0" y="67">{{ framework.name }}</text>

      <rect
        x="136"
        y="0"
        :width="index === 3 ? 516 : framework.shared ? 508 : 218"
        :height="index === 3 ? 132 : 92"
        class="engine-frame"
      />
      <image
        :href="
          index < 2 ? framework.logo : index === 3 ? '/nuxt.svg' : '/vite.svg'
        "
        x="149"
        y="5"
        width="24"
        height="24"
        :class="{ mono: index !== 2 }"
      />
      <text x="184" y="26">
        {{ index === 2 ? "Vite" : framework.name }}
      </text>

      <template v-if="index === 3">
        <rect x="144" y="32" width="500" height="92" />
        <image href="/nitro.svg" x="153" y="37" width="24" height="24" />
        <text x="188" y="58">Nitro (v2)</text>
      </template>

      <g :transform="index === 3 ? 'translate(0 32)' : undefined">
        <rect
          :x="index === 3 ? 152 : 144"
          y="34"
          :width="index === 3 ? 194 : 202"
          height="50"
        />
        <image
          v-if="index !== 3"
          :href="index < 2 ? '/vite.svg' : framework.logo"
          x="153"
          y="45"
          width="28"
          height="28"
          :class="{ mono: index === 2 }"
        />
        <text x="254" y="67" text-anchor="middle">
          {{ index < 2 ? "Vite" : index === 3 ? "builder" : framework.name }}
        </text>
        <template v-if="index === 2">
          <path d="M354 59H363m-4-4 4 4-4 4" />
          <text x="397" y="65" text-anchor="middle" class="arrow-label">
            server
          </text>
          <path d="M429 59H437m-4-4 4 4-4 4" />
        </template>
        <template v-else>
          <text x="395" y="43" text-anchor="middle" class="arrow-label">
            server
          </text>
          <path d="M354 59H436m-7-5 7 5-7 5" />
        </template>

        <rect x="444" y="34" width="192" height="50" />
        <image
          href="/zurich-cloud.svg"
          x="482"
          y="37"
          width="116"
          height="18"
        />
        <text x="540" y="76" text-anchor="middle">
          {{ framework.integration }}
        </text>
        <path
          :d="
            index === 3
              ? 'M663 59H677m-7-5 7 5-7 5'
              : 'M655 59H673m-7-5 7 5-7 5'
          "
        />
        <text x="754" y="53" text-anchor="middle" class="function">
          ZurichCloud
        </text>
        <text x="754" y="81" text-anchor="middle" class="function">
          Functions
        </text>
      </g>
    </g>
  </svg>
</template>

<style scoped>
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
path {
  fill: none;
  stroke: #94a3b8;
  stroke-width: 1.5;
}
.engine-frame {
  fill: #11151b;
}
.mono {
  filter: brightness(0) invert(1);
}
.function {
  fill: #67e8f9;
}
.arrow-label {
  fill: #c4b5fd;
  font-size: 20px;
}
.row {
  opacity: 0;
  transition: opacity 450ms ease;
}
.row.visible {
  opacity: 1;
}
@media (prefers-reduced-motion: reduce) {
  .row {
    transition: none;
  }
}
</style>
