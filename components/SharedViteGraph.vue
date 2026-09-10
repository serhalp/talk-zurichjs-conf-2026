<script setup lang="ts">
import { computed } from "vue";

const props = withDefaults(
  defineProps<{
    platforms?: boolean;
    revealed?: boolean;
    deploymentTargets?: boolean;
    focusVite?: boolean;
    pluginsOnly?: boolean;
  }>(),
  {
    platforms: false,
    revealed: true,
    deploymentTargets: undefined,
    focusVite: false,
  },
);
const frameworks = [
  { name: "Astro", logo: "/astro.svg" },
  { name: "SvelteKit", logo: "/svelte.svg" },
  { name: "React Router", logo: "/reactrouter.svg" },
  { name: "TanStack Start", logo: "/tanstack.svg" },
  { name: "SolidStart", logo: "/solid.svg" },
];
const shownFrameworks = computed(() =>
  props.pluginsOnly ? frameworks.slice(2) : frameworks,
);
</script>

<template>
  <svg
    :viewBox="
      deploymentTargets !== undefined
        ? '0 0 868 292'
        : platforms
          ? '0 0 868 265'
          : '0 0 868 180'
    "
    role="img"
    :aria-label="
      platforms
        ? 'Participating frameworks share Vite contracts consumed by a plugin for each platform'
        : 'Frameworks share Vite for client builds, server builds, and development, with deployment platforms participating through Vite'
    "
  >
    <g
      v-for="(framework, index) in shownFrameworks"
      :key="framework.name"
      :transform="`translate(${props.pluginsOnly ? 144 + index * 290 : 84 + index * 175}, 0)`"
      class="reveal"
      :class="{ faded: focusVite }"
    >
      <image :href="framework.logo" x="-22" y="0" width="44" height="44" />
      <text x="0" y="75" text-anchor="middle" class="framework-name">
        {{ framework.name }}
      </text>
      <path
        d="M0 90V102m-5-7 5 7 5-7"
        class="arrow reveal"
        :class="{ 'is-hidden': !revealed }"
      />
    </g>
    <g
      class="reveal vite-layer"
      :class="{ 'is-hidden': !revealed, focused: focusVite }"
    >
      <rect x="4" y="110" width="860" height="62" rx="12" class="box" />
      <image v-if="!platforms" href="/vite.svg" x="28" y="120" width="42" height="42" />
      <text v-if="!platforms" x="86" y="152" class="vite-name">Vite</text>
      <foreignObject v-if="platforms" x="4" y="110" width="860" height="62">
        <div xmlns="http://www.w3.org/1999/xhtml" class="vite-glue">
          <img src="/vite.svg" alt="" />
          <span class="vite-name">Vite</span>
          <span class="glue-label">🧴 Glue?</span>
        </div>
      </foreignObject>
      <g v-else>
        <g
          v-for="(label, index) in ['Client build', 'Server build', 'Dev']"
          :key="label"
          :transform="`translate(${225 + index * 205}, 0)`"
        >
          <rect
            x="0"
            y="121"
            width="190"
            height="40"
            rx="6"
            class="capability"
          />
          <text x="95" y="149" text-anchor="middle" class="detail">
            {{ label }}
          </text>
        </g>
      </g>
    </g>
    <g v-if="platforms" class="reveal" :class="{ faded: focusVite }">
      <g
        v-for="(name, index) in [
          'Netlify plugin',
          'Cloudflare plugin',
          'ZurichCloud plugin',
        ]"
        :key="name"
        :transform="`translate(${index * 292}, 0)`"
      >
        <path d="M142 174v28m-5-7 5 7 5-7" class="arrow" />
        <rect x="4" y="210" width="274" height="52" rx="8" class="box" />
        <image
          v-if="index < 2"
          :href="index === 0 ? '/netlify.svg' : '/cloudflare.svg'"
          x="17"
          y="222"
          width="28"
          height="28"
        />
        <g v-else>
          <path d="M18 223H44V249Z" fill="#f8fafc" />
          <path d="M18 223 44 249H18Z" fill="#268bcc" />
        </g>
        <text x="56" y="244" class="detail">
          {{ name }}
        </text>
      </g>
    </g>
    <g
      v-if="deploymentTargets !== undefined"
      class="reveal"
      :class="{ 'is-hidden': !deploymentTargets, faded: focusVite }"
    >
      <g
        v-for="(name, index) in [
          'Netlify',
          'Cloudflare',
          'Vercel',
          'ZurichCloud',
        ]"
        :key="name"
        :transform="`translate(${index * 218}, 0)`"
      >
        <path d="M107 174v28m-5-7 5 7 5-7" class="arrow" />
        <rect x="4" y="210" width="206" height="78" rx="8" class="box" />
        <image
          v-if="index < 2"
          :href="index === 0 ? '/netlify.svg' : '/cloudflare.svg'"
          x="93"
          y="220"
          width="28"
          height="28"
        />
        <path v-else-if="index === 2" d="M107 220 122 247H92Z" fill="#f8fafc" />
        <g v-else>
          <path d="M94 221H120V247Z" fill="#f8fafc" />
          <path d="M94 221 120 247H94Z" fill="#268bcc" />
        </g>
        <text x="107" y="274" text-anchor="middle" class="detail">
          {{ name }}
        </text>
      </g>
    </g>
  </svg>
</template>

<style scoped>
svg {
  width: 100%;
  overflow: visible;
}
text {
  fill: #f8fafc;
  font-family: inherit;
}
.framework-name {
  font-size: 24px;
}
image[href="/astro.svg"],
image[href="/svelte.svg"],
image[href="/reactrouter.svg"] {
  filter: brightness(0) invert(1);
}
.vite-name {
  font-size: 30px;
}
.vite-glue { display: flex; align-items: center; justify-content: center; gap: 16px; height: 100%; color: #f8fafc; }
.vite-glue img { width: 42px; height: 42px; }
.glue-label { margin-left: 12px; font-size: 24px; }
.detail {
  font-size: 24px;
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
.capability {
  fill: #101826;
  stroke: #64748b;
}
.reveal {
  transition: opacity 500ms ease;
}
.faded {
  opacity: 0.22;
}
.vite-layer > .box {
  transition:
    stroke 500ms ease,
    fill 500ms ease;
}
.vite-layer.focused > .box {
  stroke: #bef264;
  fill: #202b18;
}
.is-hidden {
  opacity: 0;
}
@media (prefers-reduced-motion: reduce) {
  .reveal,
  .vite-layer > .box {
    transition: none;
  }
}
</style>
