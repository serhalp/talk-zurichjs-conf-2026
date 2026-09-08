---
class: authored future-section
clicks: 11
---

<div class="matrix-main-content" :class="{ 'meme-hidden': $clicks === 8 }">

# We keep writing the same glue.

<AdapterMatrix :step="$clicks >= 8 ? $clicks - 1 : $clicks" :expansion-delay="600" />

</div>

<div class="matrix-final-form" :class="{ 'meme-hidden': $clicks !== 8 }">
  <img src="/final-form.png" alt="You fool. This isn't even my final form!" />
</div>

<style>
.matrix-main-content, .matrix-final-form { transition: opacity 350ms ease; }
.matrix-final-form { position: absolute; inset: 0; display: grid; place-items: center; pointer-events: none; }
.matrix-final-form img { width: 623px; max-height: 85%; object-fit: contain; }
.meme-hidden { opacity: 0; pointer-events: none; }
@media (prefers-reduced-motion: reduce) {
  .matrix-main-content, .matrix-final-form { transition: none; }
}
</style>

<!--
- Each cell: separate codebase + package.
- Matrix shows integration work, not a support chart.
-->

---
level: 2
class: authored future-section
clicks: 3
---

# The long tail loses out

<div class="waiting-list">
  <div><span>New framework</span><span v-click="1">Only a few platforms at launch.</span></div>
  <div><span>New platform</span><span v-click="2">Only a few frameworks at launch.</span></div>
  <div><span>New feature</span><span v-click="3">Support arrives at different times.</span></div>
</div>

<p v-click="3" class="future-takeaway">The less mainstream, less funded combinations keep waiting.</p>

<style>
.waiting-list { margin-top: 50px; }
.waiting-list > div { display: grid; grid-template-columns: 280px 1fr; gap: 20px; padding: 24px 0; border-bottom: 1px solid #475569; }
.waiting-list > div > span:first-child { font-size: 30px; }
.waiting-list > div > span:last-child { color: #cbd5e1; }
</style>

<!--
- Maintenance limits become user limitations.
-->

---
level: 2
class: authored future-section
clicks: 3
---

# These frameworks already share something.

<SharedViteGraph :revealed="$clicks >= 1" :deployment-targets="$clicks >= 2" :focus-vite="$clicks >= 3" />

<p v-click="3" class="future-takeaway">Vite sits between the framework and the platform.</p>

<!--
- Vite grew beyond browser bundling: server builds + dev.
-->

---
level: 2
class: authored future-section
clicks: 1
---

# Vite is ubiquitous.

<img src="/vite.svg" alt="Vite" class="absolute right-14 top-10 w-12 h-12" />
<AdapterMatrix :step="10" overview :highlight-vite="$clicks >= 1" />

<!--
- Angular: deeper integration in progress.
- Nuxt/Analog: Nitro handles the server build.
- Ember: Embroider.
-->

---
level: 2
class: authored future-section
clicks: 2
---

# Quick detour: 2 framework architectures

<IntegrationSurfaces :show-vite="$clicks >= 1" :focus="$clicks >= 2 ? 'vite' : undefined" />

<p v-click="2" class="future-takeaway">Let's start with frameworks where Vite is the integration surface.</p>

<!--
- Which API does the platform talk to? Both groups use Vite.
- Nuxt’s adapter surface is Nitro presets.
-->

---
level: 2
class: authored future-section
clicks: 4
---

# TanStack Start led us down a path...

<div class="start-realization">
  <img src="/tanstack.svg" alt="TanStack Start" />
  <span>Another framework appears.</span>
  <span v-click="1">Another Vite plugin for each platform.</span>
</div>

<p v-click="2" class="big-line" style="font-size: 30px">How much of this code is actually specific to TanStack Start?</p>
<div v-click="3" class="start-thought">
  <div>As a thought experiment, we tried implementing this with <em>as few TanStack Start-isms as possible</em>.</div>
  <div v-click="4" class="start-thought-question">What remains? Why?</div>
</div>

<style>
.start-realization { display: flex; align-items: center; gap: 16px; margin: 60px 0 35px; }
.start-realization img { width: 72px; height: 72px; object-fit: contain; flex-shrink: 0; }
.start-realization span { font-size: 24px; white-space: nowrap; }
.start-thought { position: relative; margin-top: 24px; padding: 18px 24px; border: 1px solid #64748b; border-radius: 18px; background: #17202e; line-height: 1.35; }
.start-thought::before, .start-thought::after { content: ''; position: absolute; border: 1px solid #64748b; border-radius: 50%; background: #17202e; }
.start-thought::before { width: 12px; height: 12px; left: 30px; bottom: -17px; }
.start-thought::after { width: 6px; height: 6px; left: 19px; bottom: -28px; }
.start-thought-question { margin-top: 12px; }
</style>

<!--
- Generic code; framework knowledge hidden in assumptions.
-->

---
level: 2
class: authored future-section platform-goal
clicks: 2
---

# Could we write just one plugin per platform?

<div class="future-status">The goal</div>
<SharedViteGraph platforms />

<p v-click="1" class="platform-roles">Frameworks describe their output via Vite.<br />Platforms adapt output via Vite.</p>
<p v-click="2" class="goal-followup">Why not?</p>

<style>
.platform-roles { font-size: 24px; line-height: 1.3; margin: 16px 0 8px; }
.platform-goal h1 { margin-bottom: 20px; }
.platform-goal .future-status { margin-bottom: 12px; }
.goal-followup { line-height: 1.3; margin: 8px 0 0; }
</style>

<!--
- Framework describes output. Platform owns deployment.
-->

---
level: 2
class: authored future-section matrix-convergence
clicks: 1
---

# What if we could share the glue?

<AdapterMatrix class="slow-convergence" :step="11" overview :converged="$clicks >= 1" />

<div class="adapter-count" :class="{ 'is-converged': $clicks >= 1 }">
  <div class="count-before"><span class="count-n">N</span><span class="count-math"> × </span><span class="count-m">M</span><span class="count-math"> = 105</span> adapters</div>
  <div class="count-after"><span class="count-m">M</span><span class="count-math"> = 7</span> adapters</div>
</div>

<style>
.adapter-count { position: absolute; bottom: 18px; left: 56px; right: 56px; text-align: center; font-size: 28px; display: grid; }
.adapter-count > div { grid-area: 1 / 1; transition: opacity 900ms ease; }
.adapter-count .count-after { opacity: 0; }
.adapter-count.is-converged > div { transition-delay: 1900ms; }
.adapter-count.is-converged .count-before { opacity: 0; }
.adapter-count.is-converged .count-after { opacity: 1; }
.adapter-count .count-n { color: #c4b5fd; font-family: var(--slidev-code-font-family); }
.adapter-count .count-m { color: #93c5fd; font-family: var(--slidev-code-font-family); }
.adapter-count .count-math { font-family: var(--slidev-code-font-family); }
@media (prefers-reduced-motion: reduce) {
  .adapter-count > div { transition: none !important; }
}
</style>

<!--
- Framework declarations still needed.
- One platform implementation, reused across frameworks.
-->

---
level: 2
class: authored future-section
clicks: 2
---

# We started comparing notes.

<div class="vite-collaborators">
  <div><img src="/netlify.svg" alt="" />Netlify</div>
  <div><img src="/cloudflare.svg" alt="" />Cloudflare</div>
  <div><img src="/tanstack.svg" alt="" />TanStack</div>
  <div v-click="1"><img src="/vite.svg" alt="" />Vite</div>
</div>

<p v-click="1" class="big-line">What belongs in Vite? What information is missing?</p>
<p v-click="2" class="future-aside" style="line-height: 1.8">🤝 We agreed on the vision.<br />And dug in...</p>

<style>
.vite-collaborators { display: flex; justify-content: space-around; gap: 28px; margin: 48px 0 32px; }
.vite-collaborators > div { display: flex; flex-direction: column; align-items: center; gap: 16px; font-size: 30px; }
.vite-collaborators img { width: 64px; height: 64px; object-fit: contain; }
</style>

<!--
- Thank the Vike/Photon folks: Universal Deploy + their help.
- Acknowledge Nitro’s cross-framework deployment work.
-->

---
level: 2
class: authored future-section
clicks: 4
---

# 4 gaps preventing this vision today

<div class="contract-needs">
  <div v-click="1"><span>1</span><p>Where are the request entry points?</p></div>
  <div v-click="2"><span>2</span><p>How do we invoke them?</p></div>
  <div v-click="3"><span>3</span><p>Which requests get routed where?</p></div>
  <div v-click="4"><span>4</span><p>How do frameworks and platforms coordinate... the rest?</p></div>
</div>

<style>
.contract-needs { margin-top: 34px; }
.contract-needs > div { display: flex; align-items: center; gap: 22px; padding: 16px 0; }
.contract-needs > div > span { display: grid; place-items: center; width: 46px; height: 46px; border: 1px solid #94a3b8; border-radius: 50%; font-family: var(--slidev-code-font-family); color: #bef264; }
.contract-needs p { margin: 0; font-size: 30px; }
</style>

<!--
- Discovery + invocation go together. Routing still open.
-->
