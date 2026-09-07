<script setup lang="ts">
import { computed, onBeforeUnmount, ref, watch } from "vue";

const props = defineProps<{
  step: number;
  overview?: boolean;
  highlightVite?: boolean;
  converged?: boolean;
  expansionDelay?: number;
}>();
const step = ref(props.step === 8 && props.expansionDelay ? 7 : props.step);
let expansionTimer: ReturnType<typeof setTimeout> | undefined;
watch(
  () => props.step,
  (next) => {
    clearTimeout(expansionTimer);
    if (next === 8 && props.expansionDelay) {
      expansionTimer = setTimeout(() => {
        step.value = next;
      }, props.expansionDelay);
    } else step.value = next;
  },
  { immediate: true },
);
onBeforeUnmount(() => clearTimeout(expansionTimer));
const frameworks = [
  { name: "Astro", logo: "/astro.svg", mono: true },
  { name: "SvelteKit", logo: "/svelte.svg", mono: true },
  { name: "React Router", logo: "/reactrouter.svg", mono: true },
  { name: "TanStack Start", logo: "/tanstack.svg" },
  { name: "Waku", logo: "/waku.svg" },
  { name: "Next.js", logo: "/nextjs.svg", mono: true },
  { name: "Nuxt", logo: "/nuxt.svg", mono: true },
  { name: "SolidStart", logo: "/solid.svg" },
  { name: "Angular", logo: "/angular.svg", mono: true },
  { name: "Qwik", logo: "/qwik.svg", mono: true },
  { name: "Analog", logo: "/analog.svg", mono: true },
  { name: "Fresh", logo: "/fresh.svg" },
  { name: "Cedar", logo: "/cedar.png" },
  { name: "Hydrogen", logo: "/hydrogen.svg", mono: true },
  { name: "Ember", logo: "/ember.svg" },
];
const platforms = [
  { name: "Netlify", logo: "/netlify.svg" },
  { name: "Cloudflare", logo: "/cloudflare.svg" },
  { name: "Vercel", logo: "" },
  { name: "ZurichCloud", logo: "zurich" },
  { name: "Deno Deploy", logo: "/deno.svg" },
  { name: "AWS Amplify", logo: "/aws-amplify.svg" },
  { name: "Firebase App Hosting", logo: "/firebase.svg" },
];
const compact = computed(() => step.value >= 8);
const wakuCells = ref(0);
const zurichCells = ref(0);
const rowCount = ref(5);
const columnCount = ref(4);
const growthDone = ref(false);
const vercelReady = ref(false);
let timers: ReturnType<typeof setTimeout>[] = [];
function clearTimers() {
  timers.forEach(clearTimeout);
  timers = [];
}
function later(delay: number, action: () => void) {
  timers.push(setTimeout(action, delay));
}
watch(
  step,
  (step) => {
    clearTimers();
    wakuCells.value = step > 6 ? 3 : 0;
    zurichCells.value = step > 7 ? 5 : 0;
    rowCount.value = step > 8 ? frameworks.length : 5;
    columnCount.value = step > 8 ? platforms.length : 4;
    growthDone.value = step > 8;
    vercelReady.value = step > 3;
    if (step === 3)
      later(350, () => {
        vercelReady.value = true;
      });
    if (step === 6) {
      for (let i = 1; i <= 3; i++)
        later(650 + (i - 1) * 550, () => {
          wakuCells.value = i;
        });
    }
    if (step === 7) {
      for (let i = 1; i <= 5; i++)
        later(650 + (i - 1) * 450, () => {
          zurichCells.value = i;
        });
    }
    if (step === 8) {
      const additions = [
        "row",
        "row",
        "row",
        "column",
        "row",
        "row",
        "row",
        "column",
        "row",
        "row",
        "row",
        "column",
        "row",
      ];
      additions.forEach((axis, i) =>
        later(1050 + i * 420, () => {
          if (axis === "row") rowCount.value++;
          else columnCount.value++;
        }),
      );
      later(1050 + additions.length * 420 + 450, () => {
        growthDone.value = true;
      });
    }
  },
  { immediate: true },
);
onBeforeUnmount(clearTimers);

const rowVisible = (row: number) =>
  row === 0 ||
  (row < 4 && step.value >= 2) ||
  (row === 4 && step.value >= 6) ||
  (compact.value && row < rowCount.value);
const columnVisible = (column: number) =>
  column === 0 ||
  (column === 1 && step.value >= 3) ||
  (column === 2 && vercelReady.value) ||
  (column === 3 && step.value >= 7) ||
  (compact.value && column < columnCount.value);
const cellVisible = (row: number, column: number) =>
  step.value > 0 &&
  rowVisible(row) &&
  columnVisible(column) &&
  !(step.value === 6 && row === 4 && column >= wakuCells.value) &&
  !(step.value === 7 && column === 3 && row >= zurichCells.value);
const cx = (column: number) =>
  compact.value ? 242 + column * 90 : 327 + column * 154;
const cy = (row: number) => (compact.value ? 66 + row * 19.5 : 96 + row * 44);
const pluginY = (column: number) => 66 + column * 42;
const rowNumberVisible = (row: number) =>
  step.value >= 7 &&
  rowVisible(row) &&
  (step.value !== 7 || row < zurichCells.value);
const columnNumberVisible = (column: number) =>
  step.value >= 6 &&
  columnVisible(column) &&
  (step.value !== 6 || column < wakuCells.value);
</script>

<template>
  <div class="matrix-story" :class="{ compact, converged }">
    <svg
      :viewBox="compact ? '0 0 868 368' : '0 0 868 330'"
      role="img"
      aria-label="A growing matrix counts a separate integration for every framework and platform combination"
    >
      <g class="convergence-layer reveal" :class="{ 'is-hidden': !converged }">
        <path
          v-for="(framework, row) in frameworks.filter(
            (f) => f.name !== 'Next.js',
          )"
          :key="framework.name"
          :d="`M206 ${cy(frameworks.indexOf(framework))}h18m-5-4 5 4-5 4`"
          class="shared-arrow"
        />
        <rect
          x="232"
          y="51"
          width="115"
          height="299"
          rx="12"
          class="shared-vite"
        />
        <image href="/vite.svg" x="269" y="125" width="42" height="42" />
        <text x="290" y="204" text-anchor="middle" class="shared-vite-name">
          Vite
        </text>
        <text x="290" y="244" text-anchor="middle" class="shared-label">
          🧴
        </text>
        <text x="290" y="268" text-anchor="middle" class="shared-label">
          Glue?
        </text>
        <path
          v-for="(_, column) in platforms"
          :key="column"
          :d="`M355 ${pluginY(column)}h42m-6-5 6 5-6 5`"
          class="shared-arrow"
        />
        <text x="460" y="27" text-anchor="middle" class="shared-label">
          Plugin
        </text>
      </g>
      <g
        v-for="(framework, row) in frameworks"
        :key="framework.name"
        class="reveal"
        :class="{
          'outside-contract': converged && framework.name === 'Next.js',
        }"
      >
        <g class="move" :style="{ transform: `translate(0px, ${cy(row)}px)` }">
          <text
            x="8"
            :y="compact ? 5 : 8"
            text-anchor="middle"
            class="count row-axis reveal"
            :class="{ 'is-hidden': !rowNumberVisible(row) }"
          >
            {{ row + 1 }}
          </text>
        </g>
        <g
          class="move"
          :class="{ 'is-hidden': !rowVisible(row) }"
          :style="{
            transform:
              row === 0 && step === 0
                ? 'translate(352px, 85px) scale(2.4)'
                : `translate(${compact ? 35 : step >= 7 ? 46 : 16}px, ${cy(row)}px) scale(${compact ? 0.48 : 1})`,
          }"
        >
          <image
            :href="framework.logo"
            x="-15"
            y="-15"
            width="30"
            height="30"
            :class="{ monochrome: framework.mono }"
          />
        </g>
        <g
          class="move"
          :style="{
            transform: `translate(${compact ? 53 : step >= 7 ? 76 : 56}px, ${cy(row)}px)`,
          }"
        >
          <text
            :y="compact ? 5 : 8"
            class="axis-name reveal"
            :class="{
              'is-hidden': step === 0 || !rowVisible(row),
              'vite-row':
                highlightVite &&
                framework.name !== 'Next.js' &&
                framework.name !== 'Angular',
              'vite-pending': highlightVite && framework.name === 'Angular',
            }"
          >
            {{ framework.name }}
          </text>
        </g>
      </g>
      <g v-for="(platform, column) in platforms" :key="platform.name">
        <g
          class="move"
          :style="{
            transform: converged
              ? `translate(842px, ${pluginY(column) + 18}px)`
              : `translate(${cx(column)}px, 0px)`,
          }"
        >
          <text
            y="-10"
            text-anchor="middle"
            class="count column-axis reveal"
            :class="{ 'is-hidden': !columnNumberVisible(column) }"
          >
            {{ column + 1 }}
          </text>
        </g>
        <g
          class="move"
          :class="{ 'is-hidden': !columnVisible(column) }"
          :style="{
            transform:
              column === 0 && step === 0
                ? 'translate(516px, 85px) scale(2.4)'
                : converged
                  ? `translate(553px, ${pluginY(column)}px) scale(.85)`
                  : `translate(${cx(column)}px, ${compact ? 13 : 19}px) scale(${compact ? 0.65 : 1})`,
          }"
        >
          <g v-if="platform.logo === 'zurich'">
            <path d="M-15-15H15V15Z" fill="white" />
            <path d="M-15-15 15 15H-15Z" fill="#268bcc" />
          </g>
          <image
            v-else-if="platform.logo"
            :href="platform.logo"
            x="-16"
            y="-16"
            width="32"
            height="32"
          />
          <path v-else fill="currentColor" d="M0-15 17 15H-17Z" />
        </g>
        <g
          class="move"
          :style="{
            transform: converged
              ? `translate(580px, ${pluginY(column) + 7}px)`
              : `translate(${cx(column)}px, ${compact ? 44 : 61}px)`,
          }"
        >
          <text
            :text-anchor="converged ? 'start' : 'middle'"
            class="axis-name platform-name reveal"
            :class="{ 'is-hidden': step === 0 || !columnVisible(column) }"
          >
            <template v-if="compact && column >= 4 && !converged">
              <tspan x="0" dy="-7">
                {{ column === 4 ? "Deno" : column === 5 ? "AWS" : "Firebase" }}
              </tspan>
              <tspan x="0" dy="15">
                {{
                  column === 4
                    ? "Deploy"
                    : column === 5
                      ? "Amplify"
                      : "App Hosting"
                }}
              </tspan>
            </template>
            <template v-else>{{ platform.name }}</template>
          </text>
        </g>
      </g>
      <g
        v-for="(framework, row) in frameworks"
        :key="`${framework.name}-cells`"
      >
        <g
          v-for="(platform, column) in platforms"
          :key="platform.name"
          class="cell move"
          :class="{
            'is-hidden': !cellVisible(row, column),
            'merged-duplicate': converged && row > 0,
            highlighted:
              (step === 9 &&
                !overview &&
                framework.name === 'TanStack Start') ||
              (step >= 10 && !overview && platform.name === 'ZurichCloud') ||
              (step === 4 && row === 1 && column === 1) ||
              (step === 5 && row === 2 && column === 2),
            'vite-row':
              highlightVite &&
              framework.name !== 'Next.js' &&
              framework.name !== 'Angular',
            'vite-pending': highlightVite && framework.name === 'Angular',
          }"
          :style="{
            transform: `translate(${converged ? 460 : cx(column)}px, ${converged ? pluginY(column) : cy(row)}px)`,
          }"
        >
          <rect
            :x="converged ? -54 : compact ? -39 : -71"
            :y="converged ? -16 : compact ? -7 : -18"
            :width="converged ? 108 : compact ? 78 : 142"
            :height="converged ? 32 : compact ? 14 : 36"
            :rx="compact ? 3 : 6"
          />
          <text
            v-if="row !== 0 || column !== 0"
            :y="converged ? 7 : compact ? 4 : 8"
            text-anchor="middle"
            class="code"
          >
            { }
          </text>
        </g>
      </g>
      <g
        class="move"
        :style="{
          transform:
            step === 0
              ? 'translate(434px, 185px)'
              : converged
                ? `translate(460px, ${pluginY(0) + 7}px)`
                : `translate(${cx(0)}px, ${cy(0) + (compact ? 4 : 8)}px)`,
        }"
      >
        <text
          text-anchor="middle"
          class="code package-name reveal"
          :class="{ 'is-hidden': step > 0 }"
        >
          @astrojs/netlify
        </text>
        <text
          text-anchor="middle"
          class="code origin-braces reveal"
          :class="{
            'is-hidden': step === 0,
            lime: highlightVite,
          }"
        >
          { }
        </text>
      </g>
      <g class="reveal" :class="{ 'is-hidden': step !== 4 && step !== 5 }">
        <rect
          x="428"
          y="276"
          width="440"
          height="49"
          rx="8"
          class="package-box"
        />
        <text x="648" y="308" text-anchor="middle" class="code lime">
          {{
            step === 5 ? "@vercel/react-router" : "@sveltejs/adapter-cloudflare"
          }}
        </text>
      </g>
      <g class="reveal" :class="{ 'is-hidden': !growthDone || converged }">
        <text x="8" y="360" text-anchor="middle" class="count row-axis">N</text>
        <text x="52" y="356">…</text>
        <text x="870" y="-10" text-anchor="middle" class="count column-axis">
          M
        </text>
        <text x="870" y="44" text-anchor="middle">…</text>
      </g>
    </svg>
    <div v-if="!overview" class="matrix-caption">
      <span v-if="step === 4 || step === 5"
        >Each square is an entire separate codebase.<br />An entire separate npm
        package.</span
      >
      <span v-else-if="step === 6"
        >New framework? Another row of integrations.</span
      >
      <span v-else-if="step === 7">New platform? Another column.</span>
      <span v-else-if="step === 9"
        >New framework feature? Update all
        <span class="axis-symbol column-axis">M</span> platform
        integrations.</span
      >
      <span v-else-if="step >= 10"
        >New platform feature? Update all
        <span class="axis-symbol row-axis">N</span> framework
        integrations.</span
      >
      <span v-else-if="growthDone"
        >We have an <span class="axis-symbol row-axis">N</span> ×
        <span class="axis-symbol column-axis">M</span> problem.</span
      >
    </div>
  </div>
</template>

<style scoped>
svg {
  width: 100%;
  overflow: visible;
  color: #f8fafc;
}
text {
  fill: currentColor;
  font-family: inherit;
  font-size: 24px;
  transition: font-size 800ms ease;
}
.code,
.count,
.axis-symbol {
  font-family: var(--slidev-code-font-family);
}
.lime {
  fill: #bef264;
}
.package-name {
  font-size: 30px;
}
.monochrome {
  filter: brightness(0) invert(1);
}
.move {
  transition:
    transform 950ms cubic-bezier(0.22, 1, 0.36, 1),
    opacity 350ms ease;
}
.reveal {
  transition: opacity 350ms ease;
}
.is-hidden {
  opacity: 0;
  pointer-events: none;
}
.cell rect {
  fill: #17202e;
  stroke: #475569;
  transition:
    x 800ms ease,
    y 800ms ease,
    width 800ms ease,
    height 800ms ease,
    stroke 400ms ease;
}
.cell text {
  fill: #cbd5e1;
}
.cell.highlighted rect,
.package-box {
  stroke: #bef264;
}
.cell.highlighted text {
  fill: #bef264;
}
.cell.vite-row rect {
  stroke: #bef264;
}
.cell.vite-row text,
text.vite-row {
  fill: #bef264;
}
.cell.vite-pending rect {
  stroke: #fcd34d;
}
.cell.vite-pending text,
text.vite-pending {
  fill: #fcd34d;
}
.package-box {
  fill: #17202e;
}
.compact .axis-name {
  font-size: 17px;
}
.compact .platform-name {
  font-size: 15px;
}
.compact .count {
  font-size: 16px;
}
.compact .cell .code,
.compact .origin-braces {
  font-size: 10px;
}
.matrix-caption {
  display: flex;
  align-items: center;
  margin-top: 12px;
  line-height: 1.3;
  min-height: 32px;
}
.convergence-layer:not(.is-hidden) {
  transition-delay: 650ms;
}
.cell.merged-duplicate {
  opacity: 0;
  transition-delay: 0ms, 600ms;
}
.outside-contract {
  opacity: 0.25;
}
.shared-arrow {
  fill: none;
  stroke: #94a3b8;
  stroke-width: 1.2;
  stroke-linecap: round;
  stroke-linejoin: round;
}
.shared-vite {
  fill: #202b18;
  stroke: #bef264;
  stroke-width: 1.5;
}
.shared-vite-name {
  font-size: 30px;
}
.shared-label {
  font-size: 20px;
}
.converged .platform-name {
  font-size: 22px;
}
.converged .cell .code,
.converged .origin-braces {
  font-size: 20px;
}
.row-axis {
  color: #c4b5fd;
  fill: #c4b5fd;
}
.column-axis {
  color: #93c5fd;
  fill: #93c5fd;
}
.slow-convergence .move {
  transition-duration: 1700ms, 600ms;
  transition-timing-function: ease-in-out, ease;
}
.slow-convergence .reveal {
  transition-duration: 600ms;
}
.slow-convergence .cell rect,
.slow-convergence text {
  transition-duration: 1700ms;
  transition-timing-function: ease-in-out;
}
.slow-convergence .convergence-layer:not(.is-hidden) {
  transition-delay: 1100ms;
}
.slow-convergence .cell.merged-duplicate {
  transition-delay: 0ms, 1100ms;
}
@media (prefers-reduced-motion: reduce) {
  .move,
  .reveal,
  .cell rect,
  text {
    transition: none !important;
  }
}
</style>
