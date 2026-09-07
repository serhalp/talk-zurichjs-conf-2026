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
The fourth bucket. The scope discussion separates request fulfillment from other platform configuration. Framework adapters can carry such configuration, or a framework may deliberately leave it to users to configure directly on their platform.
After the initial list, clicks 5–8 focus Image CDN / redirects and rewrites / static response headers / skew protection respectively. Fade the other rows and show one example and verdict at a time. The image code is hidden until click 5. The NO / maybe / maybe / rainbow no idea badges are Philippe's spoken positioning on Vite core scope, not assertions that a platform or framework lacks these features. The tiny skew diagram shows an old tab reaching its matching server while a newer deployment exists; the fuller explanation follows later.
For a framework implemented purely as a Vite plugin, exposing these features requires another communication channel. That is a design choice to make explicitly, not an argument that every framework must hide the platform.
Source: https://github.com/vitejs/ecosystem/issues/3
The image excerpt uses Astro's real image.remotePatterns setting to authorize remote image optimization. The surrounding defineConfig call is omitted. A deployment adapter can translate this intent into platform Image CDN configuration; this is not itself a platform API. Source checked September 7: https://docs.astro.build/en/guides/images/#authorizing-remote-images
Redirects/rewrites and static response headers are distinct rows. Their placement here is a discussion aid, not an assertion redirects cannot belong to routing. The final …? invites consideration of further cases rather than claiming this list is exhaustive.
The redirect example uses real Nuxt routeRules, with defineNuxtConfig omitted. The shorthand uses Nitro's default redirect status; no specific status is claimed on the slide. Sources checked September 7: https://nuxt.com/docs/4.x/guide/concepts/rendering ; https://v2.nitro.build/config#routerules
The headers example also uses Nuxt routeRules. Keep familiar frameworks here; using Nuxt twice is preferable to introducing Vike just for variety. This is framework configuration, not a raw HTTP response. Source: https://v2.nitro.build/config#routerules
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
The arrows show configuration/integration relationships, not runtime request flow. Green arrows show available connections; a red broken arrow marks Vite plugin → framework as Vite plugin, where the framework-specific adapter surface is absent. Start with Web developer, SvelteKit, Vite, the ZurichCloud SvelteKit adapter, and ZurichCloud. Click 1 draws developer connections in sequence. Click 2 adds SvelteKit → Vite. Click 3 draws adapter → SvelteKit, Vite, ZurichCloud. Click 4 introduces TanStack Start with developer → TanStack Start → Vite, fading the SvelteKit side. Click 5 introduces the ZurichCloud Vite plugin and its developer, Vite, and platform connections. Click 6 shows the straight red broken connection to TanStack Start. Click 7 restores the SvelteKit side for comparison.
Compare framework as Vite plugin (TanStack) with framework with adapters (SvelteKit). The web developer connects directly to both frameworks, Vite, both platform integrations, and ZurichCloud. Both frameworks point into shared Vite. Both platform integrations point UP into Vite and DOWN into ZurichCloud.
The distinguishing connection is ZurichCloud adapter → framework with adapters, running straight up beside Vite. The adapter has a framework-specific integration API; the generic Vite plugin only has the shared Vite surface. This is an integration-surface comparison, not a claim JavaScript plugins are literally incapable of communicating.
The cat represents the web developer. No Tanner photo or config-filename annotations. The developer → Vite connection runs straight down between the two frameworks, keeping it clear of the red broken arrow.
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
Connect the interaction diagram to a deliberate framework design choice. We can choose not to expose every platform feature as framework configuration. This is one possible boundary, not a claim that these features must be configured this way or never need coordination.
Start with the same four features. Click 1 moves Image CDN configuration into “Configure on the platform.” Click 2 moves redirects/rewrites. Click 3 moves static response headers. Users can configure those directly if the framework leaves them out of its own surface; framework-generated routing/header requirements are a separate matter.
Click 4 fades that choice and highlights skew protection. For the strategy we're exploring, the platform provides a deployment identifier and supported request carriers; the framework needs to attach that metadata to the requests its generated client code makes. Platform configuration alone cannot express that whole interaction. The next slide proposes a communication contract outside Vite core.
This does not claim every skew-protection implementation requires the same mechanism. It motivates the coordinated approach in proposed VDM0001: https://github.com/vitejs/deployment-metadata/blob/db8dc777a405dfca0f65af8b883c5f56c8c8e9fa/metadata/proposed/VDM0001/spec.md
-->
