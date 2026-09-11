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
<div class="metadata-verdict-row">
<span class="framework-aside metadata-verdict-question"><svg class="aside-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M5 4h14a2 2 0 0 1 2 2v10a2 2 0 0 1-2 2H9l-5 3v-3a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2Z" /><path d="M7 9h10M7 13h6" /></svg><span>Belongs in Vite core?</span></span>
<div :key="$clicks" class="metadata-verdict" :class="$clicks === 5 ? 'verdict-no' : $clicks === 8 ? 'verdict-unknown' : 'verdict-maybe'">{{ $clicks === 5 ? 'NO' : $clicks === 8 ? 'no idea' : 'maybe' }}</div>
</div>
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

<p v-click="4" class="framework-aside metadata-bottom-aside" :class="{ 'metadata-aside-dim': $clicks >= 5 }"><svg class="aside-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M5 4h14a2 2 0 0 1 2 2v10a2 2 0 0 1-2 2H9l-5 3v-3a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2Z" /><path d="M7 9h10M7 13h6" /></svg><span>Useful platform features. Not all of them belong in Vite core.</span></p>

<style>
.metadata-examples-slide h1 { margin-bottom: 14px; }
.metadata-examples { display: grid; grid-template-columns: 345px 1fr; column-gap: 18px; margin-top: 12px; min-height: 268px; }
.metadata-item { grid-column: 1; font-size: 28px; padding: 9px 0 9px 10px; line-height: 1.3; border-left: 3px solid transparent; transition: opacity 350ms, border-color 350ms; }
.metadata-more { color: #94a3b8; }
.reviewing-features .metadata-item { opacity: .22; }
.reviewing-features .metadata-item.active { opacity: 1; border-left-color: #e2e8f0; }
.metadata-detail { grid-column: 2; grid-row: 1 / span 5; justify-self: end; align-self: start; display: grid; grid-template-columns: minmax(0, 1fr); justify-items: end; align-items: start; gap: 16px; max-width: 100%; transition: opacity 350ms; }
.metadata-example, .metadata-skew-example { grid-area: 2 / 1; }
.metadata-verdict-row { grid-area: 1 / 1; display: flex; align-items: center; gap: 16px; }
.metadata-examples-slide .metadata-verdict-question { margin-top: 0; white-space: nowrap; }
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
.metadata-examples-slide .metadata-bottom-aside { margin-top: 10px; transition: opacity 350ms; }
.metadata-aside-dim { opacity: .22; }
@keyframes verdict-in { from { opacity: 0; transform: scale(.85) rotate(-5deg); } to { opacity: 1; transform: scale(1) rotate(-2deg); } }
@keyframes metadata-example-in { from { opacity: 0; transform: translateY(5px); } to { opacity: 1; transform: translateY(0); } }
@media (prefers-reduced-motion: reduce) { .metadata-item, .metadata-detail, .metadata-bottom-aside { transition: none !important; } .metadata-verdict, .metadata-example, .metadata-skew-example { animation: none; } }
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
clicks: 5
---

# <span class="gap-number">4</span> #wontfix

<FrameworkFeatureChoice :step="$clicks" />

<style>
.feature-choice-slide h1 { margin-bottom: 22px; }
</style>

<!--
- Vite-only integration: also choosing the framework’s configuration boundary.
- A possible design choice, not a claim about the teams’ intentions.
- Skew: platform supplies deployment ID; framework tags requests.
-->

---
level: 2
class: authored future-section metadata-teaser
clicks: 4
---

# <span class="gap-number">4</span> Exploring deployment metadata

<Transition name="teaser-stage" mode="out-in">
<div v-if="$clicks < 2" key="question" class="teaser-boundary">
<p class="teaser-cake">What if we could have our cake and eat it too?</p>
<FrameworkBoundary :step="6" :metadata="$clicks >= 1" settled />
</div>
<div v-else key="metadata">

<p class="teaser-premise">A way for frameworks and platforms to coordinate.</p>

<div class="teaser-exchange">
  <div>Framework<span>What I need</span></div>
  <span class="exchange-arrow">↔</span>
  <div class="metadata-record">Deployment metadata</div>
  <span class="exchange-arrow">↔</span>
  <div>Platform<span>What I support</span></div>
</div>

<div v-click="3" class="teaser-collaboration">
  <p>Designing this together:</p>
  <div class="teaser-teams">
    <span><img src="/netlify.svg" alt="" />Netlify</span>
    <span><img src="/cloudflare.svg" alt="" />Cloudflare</span>
    <span><img src="/tanstack.svg" alt="" />TanStack</span>
    <span><img src="/vite.svg" alt="" />Vite core</span>
  </div>
</div>

<div v-click="4" class="teaser-credit"><img src="/vike.svg" alt="Vike" /><span>With help and prototyping from the Vike team,<br />behind Photon and Universal Deploy.</span></div>

<a class="teaser-link" href="https://github.com/vitejs/deployment-metadata">vitejs/deployment-metadata ↗</a>
</div>
</Transition>

<style>
.metadata-teaser .teaser-cake { margin: 16px 0 18px; font-size: 28px; }
.teaser-boundary > svg { max-height: 328px; }
.teaser-stage-enter-active, .teaser-stage-leave-active { transition: opacity 450ms ease, transform 450ms ease; }
.teaser-stage-enter-from { opacity: 0; transform: translateY(8px); }
.teaser-stage-leave-to { opacity: 0; transform: translateY(-8px); }
@media (prefers-reduced-motion: reduce) { .teaser-stage-enter-active, .teaser-stage-leave-active { transition: none; } }
.metadata-teaser .teaser-premise { margin: 24px 0; font-size: 28px; }
.teaser-exchange { display: grid; grid-template-columns: 1fr 32px 1.25fr 32px 1fr; gap: 12px; align-items: center; margin: 26px 0; }
.teaser-exchange > div { border: 1px solid #64748b; border-radius: 8px; padding: 16px 10px; text-align: center; font-size: 25px; }
.teaser-exchange > div > span { display: block; margin-top: 6px; color: #cbd5e1; font-size: 22px; }
.teaser-exchange .metadata-record { border-color: #67e8f9; color: #a5f3fc; background: #142c34; }
.exchange-arrow { color: #94a3b8; font-size: 30px; text-align: center; }
.metadata-teaser .teaser-collaboration p { margin: 0 0 12px; font-size: 24px; }
.teaser-teams { display: flex; align-items: center; justify-content: space-between; font-size: 25px; }
.teaser-teams span { display: flex; gap: 10px; align-items: center; }
.teaser-teams img { width: 32px; height: 32px; object-fit: contain; }
.metadata-teaser .teaser-credit { display: flex; align-items: center; gap: 16px; margin-top: 24px; font-size: 24px; line-height: 1.45; }
.teaser-credit img { width: 44px; height: 44px; object-fit: contain; }
.teaser-link { position: absolute; bottom: 24px; right: 56px; font-size: 20px; color: #94a3b8; }
</style>

<!--
- Still exploring; not a finished standard.
- Vike team: Photon, Universal Deploy, prototyping and help.
- More depth in the ViteConf talk next month?
-->

---
level: 2
class: authored future-section working-slide
clicks: 5
---

# Unified platform plugins, in practice

<div v-click="1" class="netlify-working" :class="{ 'with-solid': $clicks >= 2, 'with-rr': $clicks >= 4 }">
  <div class="working-platform"><img src="/netlify.svg" alt="" /><span>Netlify Vite plugin</span></div>
  <svg class="working-branches" viewBox="0 0 54 130" aria-hidden="true">
    <path :d="$clicks >= 4 ? 'M1 65H12Q20 65 20 57V26Q20 18 28 18H51m-6-5 6 5-6 5' : $clicks >= 2 ? 'M1 65H12Q20 65 20 57V42Q20 34 28 34H51m-6-5 6 5-6 5' : 'M1 65H12Q20 65 20 65V65Q20 65 28 65H51m-6-5 6 5-6 5'" />
    <path v-click="2" :d="$clicks >= 4 ? 'M1 65H51m-6-5 6 5-6 5' : 'M1 65H12Q20 65 20 73V82Q20 90 28 90H51m-6-5 6 5-6 5'" />
    <path v-click="4" class="rr-branch" d="M1 65H12Q20 65 20 73V104Q20 112 28 112H51m-6-5 6 5-6 5" />
  </svg>
  <span class="working-framework tanstack-working"><img src="/fetchable/tanstack.svg" alt="" />TanStack Start</span>
  <span class="working-site-count">Powers 100k+ sites.</span>
  <span v-click="2" class="working-framework solid-working"><img src="/fetchable/solid.svg" alt="" />SolidStart 2</span>
  <span v-click="4" class="working-framework rr-working"><img src="/reactrouter.svg" alt="" class="working-mono" />React Router <b>?</b></span>
</div>

<div class="working-proof">
  <p v-click="2" class="worked-first-try" :class="{ 'detail-hidden': $clicks >= 4 }">SolidStart 2 shipped last month. It just worked. No code changes.</p>
  <p class="worked-first-try rr-question" :class="{ 'detail-hidden': $clicks < 4 }">React Router should be doable next, but…</p>
</div>

<div v-click="3" class="working-assumptions" :class="{ 'rr-assumptions': $clicks >= 4 }">
  <strong :class="{ 'detail-hidden': $clicks >= 4 }">But we're relying on assumptions that hold for now:</strong>
  <div>
    <span><i :class="{ failed: $clicks >= 4 }">{{ $clicks >= 4 ? '✕' : '✓' }}</i>Fetchable module<small v-show="$clicks >= 4">Needs a wrapper</small></span>
    <span><i :class="{ caveat: $clicks >= 4 }">{{ $clicks >= 4 ? '△' : '✓' }}</i>One server entry point<small v-show="$clicks >= 4">Unless the user splits server bundles</small></span>
    <span><i :class="{ caveat: $clicks >= 4 }">{{ $clicks >= 4 ? '△' : '✓' }}</i>Catch-all routing<small v-show="$clicks >= 4">Custom splitting needs routing information</small></span>
    <span><i>✓</i>No extra coordination</span>
  </div>
</div>

<div v-click="5" class="cloudflare-working">
  <div class="working-platform"><img src="/cloudflare.svg" alt="" /><span>Cloudflare Vite plugin</span></div>
  <svg class="working-branches" viewBox="0 0 54 90" aria-hidden="true">
    <path d="M1 45H12Q20 45 20 37V30Q20 22 28 22H51m-6-5 6 5-6 5" />
    <path d="M1 45H12Q20 45 20 53V60Q20 68 28 68H51m-6-5 6 5-6 5" />
  </svg>
  <span class="working-framework cf-react-router"><img src="/reactrouter.svg" alt="" class="working-mono" />React Router</span>
  <span class="working-framework cf-tanstack"><img src="/fetchable/tanstack.svg" alt="" />TanStack Start</span>
</div>

<style>
.working-slide h1 { margin-bottom: 20px; }
.working-platform { display: flex; align-items: center; gap: 12px; padding: 14px; border: 1px solid #64748b; border-radius: 10px; font-size: 23px; white-space: nowrap; }
.working-platform img { width: 34px; height: 34px; object-fit: contain; }
.working-mono { filter: brightness(0) invert(1); }
.netlify-working { position: relative; height: 130px; margin-top: 8px; }
.netlify-working .working-platform { position: absolute; left: 0; top: 31px; width: 330px; }
.working-branches { position: absolute; left: 342px; top: 0; width: 54px; height: 130px; fill: none; stroke: #94a3b8; stroke-width: 1.5; }
.working-branches path { transition: d 650ms ease; }
.working-branches .rr-branch { stroke: #fcd34d; }
.working-framework { position: absolute; left: 408px; display: flex; align-items: center; gap: 10px; font-size: 23px; white-space: nowrap; transition: top 650ms ease; }
.working-framework img { width: 32px; height: 32px; object-fit: contain; }
.tanstack-working { top: 49px; }
.with-solid .tanstack-working { top: 18px; }
.solid-working { top: 74px; }
.with-rr .tanstack-working { top: 2px; }
.with-rr .solid-working { top: 49px; }
.rr-working { top: 96px; color: #fcd34d; }
.rr-working b { font-weight: 400; }
.working-site-count { position: absolute; left: 650px; top: 49px; font-size: 23px; color: #bef264; white-space: nowrap; transition: top 650ms ease; }
.with-solid .working-site-count { top: 18px; }
.with-rr .working-site-count { top: 2px; }
.working-proof { display: grid; }
.worked-first-try { grid-area: 1 / 1; margin: 8px 0; color: #bef264; font-size: 25px; line-height: 1.35; transition: opacity 400ms, visibility 400ms; }
.rr-question { color: #fcd34d; }
.detail-hidden { opacity: 0 !important; visibility: hidden !important; }
.working-assumptions { margin: 4px 0 0; font-size: 22px; }
.working-assumptions strong { display: block; max-height: 40px; font-weight: 400; color: #cbd5e1; transition: opacity 400ms, max-height 600ms; }
.rr-assumptions strong { max-height: 0; overflow: hidden; }
.working-assumptions > div { display: grid; grid-template-columns: 1fr 1fr; gap: 6px 22px; margin-top: 8px; line-height: 1.4; }
.working-assumptions > div > span { position: relative; min-height: 50px; padding-left: 28px; }
.working-assumptions i { position: absolute; left: 0; font-style: normal; color: #86b99a; font-size: 20px; }
.working-assumptions i.failed { color: #fda4af; }
.working-assumptions i.caveat { color: #fcd34d; }
.working-assumptions small { display: block; color: #cbd5e1; font-size: 18px; line-height: 1.25; }
@media (prefers-reduced-motion: reduce) { .netlify-working * { transition: none !important; } }
.cloudflare-working { position: relative; height: 90px; margin-top: 28px; }
.cloudflare-working .working-platform { position: absolute; left: 0; top: 11px; width: 330px; }
.cloudflare-working .working-branches { height: 90px; }
.cf-react-router { top: 6px; }
.cf-tanstack { top: 52px; }
</style>

<!--
- Assumptions: one Fetchable entry, all server requests routed there.
- SolidStart 2: tried it; zero framework-specific changes.
- React Router: plausible next; not Fetchable. Niche serverBundles option needs routing information.
- Cloudflare: React Router + TanStack Start, different mechanics.
- Next: delegate Astro/SvelteKit adapter code to the same plugin. Not done yet.
-->
