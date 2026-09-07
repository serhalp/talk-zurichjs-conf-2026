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
Return to the repeated work we saw before the Next.js detour. Astro × Netlify, SvelteKit × Netlify, Astro × Cloudflare: different implementations, much of the same job.
This is an illustrative responsibility matrix, NOT a claim that every cell has a released adapter. The Waku row and ZurichCloud column are examples of ecosystem growth, not release announcements.
Start with Astro + Netlify and @astrojs/netlify. Click 1 moves the same logos and package into one matrix cell, with the package abbreviated to braces. Click 2 adds SvelteKit, React Router, and TanStack Start. Click 3 adds Cloudflare and Vercel.
Clicks 4–5 highlight @sveltejs/adapter-cloudflare and @vercel/react-router in turn: separate integration codebases and npm packages, not necessarily separate Git repositories. The Vercel package supplies a React Router preset, rather than a standalone deployment implementation.
Click 6 clears the callout and adds Waku. Platform counts 1–3 appear with its cells, one after another. Click 7 adds ZurichCloud and column count 4, then counts the framework rows as that column fills from top to bottom.
Click 8 hides the slide contents and shows the final-form meme. Click 9 brings back and shrinks the matrix and automatically interleaves more frameworks with Deno Deploy, AWS Amplify, and Firebase. At the end the open-ended axes become N frameworks and M platforms: an N × M problem. This remains an illustrative responsibility matrix, not a released-support chart. Click 10 highlights TanStack Start's row: all M platform integrations. Click 11 highlights ZurichCloud's column: all N framework integrations.
Vercel package name and preset: https://vercel.com/docs/frameworks/frontend/react-router
The original RFC's N-by-M motivation and missing integrations: https://github.com/vitejs/vite/discussions/20907
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
This is the cost to users, not just an engineering-efficiency argument. Limited maintainer time means the most popular combinations tend to get attention first. It is a structural tendency, not a claim that every launch follows this exact schedule.
Keep the long tail in the story: new ideas should not need a full collection of custom adapters before people can use them.
Source and speaker's argument: https://github.com/vitejs/vite/discussions/20907
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
We have seen Vite throughout the earlier adapter examples. It handles client and server builds and local development. The Environment API gives frameworks and platform plugins a common place to configure environments and participate in their lifecycle.
The diagram shows selected Vite-based frameworks. It doesn't include Next.js and doesn't claim every framework uses Vite or delegates orchestration identically.
Sources: https://vite.dev/guide/api-environment and the scope discussion https://github.com/vitejs/ecosystem/issues/3
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
Bring back the same matrix. On click, highlight the Vite-based frameworks; Next.js remains unhighlighted. Angular is yellow for the in-progress direction Philippe will explain aloud, with no on-slide status label.
This compares their relationship to Vite, not whether every framework/platform integration exists or whether every framework uses Vite identically for dev, client builds, and server builds. Angular's current CLI integration and the direction toward deeper Vite integration should not be conflated.
Ember's modern build uses Embroider as a Vite plugin: https://guides.emberjs.com/release/build-tools/vite/
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
Name the distinction already shown in the earlier framework diagrams: which integration surface can the platform use? This is not a mutually exclusive taxonomy of frameworks as toolchains versus plugins. Astro and SvelteKit also use Vite; React Router has presets as discussed earlier. These are the integration paths we have been following in this talk.
For Astro and SvelteKit, the framework adapter API provides framework-specific information. For our React Router and TanStack Start integrations, Vite is the shared surface, so missing information becomes an obstacle there.
Nuxt's framework-side deployment integration goes through the Nitro preset API discussed earlier, rather than a Nuxt-specific adapter API. SolidStart 2 joins the Vite examples through its deployment-plugin architecture.
Waku and Qwik were considered but omitted from this deliberately simple comparison. Waku documents its own waku/adapters/* surface. Qwik calls its Vite deployment configurations adapters, and also has framework-specific request middleware; it is a mixed case rather than a clean illustration of a Vite-only integration surface. These boxes are examples, not exhaustive disjoint categories.
Sources: https://waku.gg/ ; https://qwik.dev/docs/deployments/ ; https://docs.solidjs.com/solid-start/v2/guides/deployment-plugins
Start with the Vite-plugin path. The next section asks what common contracts would let a platform plugin serve more than one framework. Return to the framework-adapter path after discovery, invocation, and routing: those adapters can declare the same information and delegate common work.
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
Recall the earlier slide: TanStack Start moved away from bundling Nitro into the framework and is implemented as a Vite plugin. Netlify's TanStack Start support provided the concrete moment of recognition.
We are deliberately following the Vite integration path first. We will return to Astro and SvelteKit's own adapter APIs after establishing the shared contracts.
Philippe's original RFC links a historical plugin with no TanStack-specific implementation logic. That was possible because it assumed which server bundle entry was the handler. It wasn't a universal contract and could not safely cover arbitrary frameworks or advanced configurations.
Use this as firsthand motivation, not a claim about the current plugin source or a guarantee that all frameworks already work.
Historical code: https://github.com/netlify/primitives/blob/413ef5dcf37c7324ce4465dd5566b0e5c5199792/packages/vite-plugin-tanstack-start/src/main.ts
RFC: https://github.com/vitejs/vite/discussions/20907
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
This is the proposed architecture, not today's universal compatibility. Each platform still owns its deployment logic. Each framework still needs to provide the shared information and target a compatible runtime.
One reusable plugin per platform does not eliminate all framework-specific adapters. Astro and SvelteKit can delegate common work to that plugin, while retaining their own adapter APIs. Nitro can also participate; this isn't an anti-Nitro proposal.
The actual reduction is toward framework declarations plus platform implementations, rather than an implementation for every pair. Avoid presenting N as a literal accounting identity that erases the framework-side work.
Scope: https://github.com/vitejs/ecosystem/issues/3
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
Start with the same full matrix. On click, its repeated cells converge into one plugin per platform; Vite provides a shared contract between participating frameworks and platform implementations.
This is the goal, not a claim that these integrations already exist. Next.js stays visible but faded, outside the Vite connections. Frameworks still need to expose the common information, and framework-specific adapter APIs can remain. Nitro and Angular's integration paths have their own caveats, discussed earlier.
The change is from pair-specific implementations toward framework-side declarations plus reusable platform implementations, not the elimination of framework-side work.
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
Philippe talked with the TanStack team, heard Cloudflare was exploring similar ideas, and compared notes with them and the Vite core team. This is a second collaboration story, now across frameworks as well as platforms.
The May 6, 2026 ecosystem call agreed the intended scope, recorded May 11 in ecosystem issue 3. That is agreement on direction, not approval or release of every proposed API. Request fulfillment belongs in Vite's scope; other platform features need a separate layer or direct configuration.
Source: https://github.com/vitejs/ecosystem/issues/3#issuecomment-4421073692
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
The original four buckets from Philippe's outline. We will solve discovery and invocation together, then explain routing, then separate the final feature bucket from Vite core.
This is not four independent finished proposals: entry point discovery and Fetchable signatures share one concrete RFC; routing remains an open design; deployment metadata is a separate effort.
Source: https://github.com/vitejs/vite/discussions/20907
-->
