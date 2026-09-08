---
class: authored future-section metadata-examples-slide
clicks: 8
---

# <span class="gap-number">4</span> How do frameworks and platforms coordinate... the rest?

<div class="metadata-examples" :class="{ 'reviewing-features': $clicks >= 5 }">
<div class="metadata-item" :class="{ active: $clicks === 5 }">Image CDN configuration</div>
<div v-click="1" class="metadata-item" :class="{ active: $clicks === 6 }">Redirects and rewrites</div>
<div v-click="2" class="metadata-item" :class="{ active: $clicks === 7 }">Static response headers</div>
<div v-click="3" class="metadata-item" :class="{ active: $clicks === 8 }">Skew protection</div>
<div v-click="4" class="metadata-item metadata-more">…?</div>

<div class="metadata-detail" :class="{ 'detail-hidden': $clicks < 5 }">
<div :key="$clicks" class="metadata-verdict" :class="$clicks === 5 ? 'verdict-no' : $clicks === 8 ? 'verdict-unknown' : 'verdict-maybe'">{{ $clicks === 5 ? 'NO' : $clicks === 8 ? 'no idea' : 'maybe' }}</div>
<div class="metadata-example" :class="{ 'example-hidden': $clicks !== 5 }">

<!-- prettier-ignore -->
```ts [astro.config.ts]
image: {
  remotePatterns: [
    { hostname: "**.example.com" },
  ],
},
```

</div>
<div class="metadata-example" :class="{ 'example-hidden': $clicks !== 6 }">

```ts [nuxt.config.ts]
routeRules: {
  "/old": { redirect: "/new" },
},
```

</div>
<div class="metadata-example" :class="{ 'example-hidden': $clicks !== 7 }">

```ts [nuxt.config.ts]
routeRules: {
  "/assets/**": {
    headers: {
      "cache-control": "max-age=3600",
    },
  },
},
```

</div>
<div class="metadata-skew-example" :class="{ 'example-hidden': $clicks !== 8 }">
<svg viewBox="0 0 410 182" role="img" aria-label="An old browser tab sends requests to its matching deployment, while a newer deployment is live.">
  <rect x="0" y="55" width="140" height="74" rx="8" />
  <path d="M0 79h140" class="skew-line" />
  <text x="70" y="73" text-anchor="middle" class="skew-small">Open tab</text>
  <text x="70" y="111" text-anchor="middle">v1</text>
  <rect x="248" y="4" width="160" height="68" rx="8" />
  <text x="328" y="32" text-anchor="middle">Server v1</text>
  <text x="328" y="58" text-anchor="middle" class="skew-small">matching version</text>
  <g class="new-deployment">
    <rect x="248" y="111" width="160" height="68" rx="8" />
    <text x="328" y="139" text-anchor="middle">Server v2</text>
    <text x="328" y="165" text-anchor="middle" class="skew-small">new deployment</text>
  </g>
  <path d="M144 96h28q16 0 16-16V56q0-18 18-18h34m-7-6 7 6-7 6" class="skew-route" />
</svg>
</div>
</div>
</div>

<p v-click="4" class="future-aside" :class="{ 'metadata-aside-dim': $clicks >= 5 }">Useful platform features. Not all of them belong in Vite core.</p>

<style>
.metadata-examples-slide h1 { margin-bottom: 14px; }
.metadata-examples { display: grid; grid-template-columns: 345px 1fr; column-gap: 18px; margin-top: 12px; min-height: 268px; }
.metadata-item { grid-column: 1; font-size: 28px; padding: 9px 0 9px 10px; line-height: 1.3; border-left: 3px solid transparent; transition: opacity 350ms, border-color 350ms; }
.metadata-more { color: #94a3b8; }
.reviewing-features .metadata-item { opacity: .22; }
.reviewing-features .metadata-item.active { opacity: 1; border-left-color: #e2e8f0; }
.metadata-detail { grid-column: 2; grid-row: 1 / span 5; justify-self: end; align-self: start; display: grid; grid-template-columns: minmax(0, 1fr); justify-items: end; align-items: start; gap: 16px; max-width: 100%; transition: opacity 350ms; }
.metadata-example, .metadata-skew-example { grid-area: 2 / 1; }
.metadata-verdict { grid-area: 1 / 1; }
.example-hidden { visibility: hidden; pointer-events: none; animation: none !important; }
.detail-hidden { opacity: 0; visibility: hidden; }
.metadata-example { width: max-content; max-width: 100%; animation: metadata-example-in 400ms ease both; }
.metadata-verdict { font-size: 28px; font-weight: 700; line-height: 1; padding: 10px 20px; border: 2px solid; border-radius: 8px; animation: verdict-in 450ms ease both; }
.verdict-no { color: #fca5a5; border-color: #f87171; background: #7f1d1d55; }
.verdict-maybe { color: #fde68a; border-color: #facc15; background: #713f123d; }
.verdict-unknown { color: #17202e; border-color: transparent; background: linear-gradient(110deg, #fda4af, #fde68a, #bef264, #67e8f9, #c4b5fd, #f0abfc); }
.metadata-skew-example { width: 410px; max-width: 100%; animation: metadata-example-in 400ms ease both; }
.metadata-skew-example svg { width: 100%; overflow: visible; }
.metadata-skew-example rect { fill: #17202e; stroke: #64748b; }
.metadata-skew-example text { font-family: inherit; fill: #f8fafc; font-size: 24px; }
.metadata-skew-example .skew-small { font-size: 19px; fill: #cbd5e1; }
.skew-line { stroke: #64748b; }
.skew-route { fill: none; stroke: #bef264; stroke-width: 2; stroke-linecap: round; stroke-linejoin: round; }
.new-deployment { opacity: .5; }
.metadata-examples-slide .future-aside { margin-top: 10px; padding: 12px 18px; transition: opacity 350ms; }
.metadata-aside-dim { opacity: .22; }
@keyframes verdict-in { from { opacity: 0; transform: scale(.85) rotate(-5deg); } to { opacity: 1; transform: scale(1) rotate(-2deg); } }
@keyframes metadata-example-in { from { opacity: 0; transform: translateY(5px); } to { opacity: 1; transform: translateY(0); } }
@media (prefers-reduced-motion: reduce) { .metadata-item, .metadata-detail, .future-aside { transition: none !important; } .metadata-verdict, .metadata-example, .metadata-skew-example { animation: none; } }
</style>

<!--
- Badges ask “Does this belong in Vite core?”
- Skew: old browser code, new server deployment.
-->

---
level: 2
class: authored future-section boundary-slide
clicks: 7
---

# <span class="gap-number">4</span> Constrained interactions

<p class="boundary-intro">Not all interactions are possible for frameworks-as-Vite-plugins</p>

<FrameworkBoundary class="boundary-diagram" :step="$clicks" />

<style>
.boundary-slide h1 { margin-bottom: 22px; }
.boundary-intro { margin: 0 0 14px; font-size: 24px; line-height: 1.35; }
.boundary-diagram { max-height: 360px; }
</style>

<!--
- Integration APIs, not HTTP traffic.
- Red arrow: no framework-specific adapter API.
- Choosing Vite also means choosing its limits.
-->

---
level: 2
class: authored future-section feature-choice-slide
clicks: 4
---

# <span class="gap-number">4</span> Leave it to the user?

<FrameworkFeatureChoice :step="$clicks" />

<p v-click="4" class="coordination-reason">The platform identifies the deployment.<br />The framework tags requests with that identifier.</p>

<style>
.feature-choice-slide h1 { margin-bottom: 22px; }
.coordination-reason { margin: 18px 0 0; font-size: 26px; line-height: 1.45; }
</style>

<!--
- Deliberate framework scope choice.
- Skew strategy: platform supplies deployment ID; framework tags requests.
-->
