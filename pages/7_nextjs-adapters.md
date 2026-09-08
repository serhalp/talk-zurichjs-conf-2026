---
layout: center
class: authored reality-interstitial
hideInToc: true
---

<div class="reality-line">Press pause on ZurichCloud for a moment.<br />Back to reality.</div>

<style>
.reality-line { font-size: 44px; line-height: 1.4; text-align: center; color: #a5f3fc; }
</style>

---
class: authored
clicks: 4
---

# We weren't the only ones doing this.

<div class="opennext-collaboration">
  <div class="adapter-teams">
    <div><span class="team-brand"><img src="/netlify.svg" alt="" />Netlify</span><small>Netlify adapter</small></div>
    <div><span class="team-brand"><img src="/cloudflare.svg" alt="" />Cloudflare</span><small>Cloudflare adapter</small></div>
    <div><span class="team-brand"><img src="/opennext.svg" alt="OpenNext" class="opennext-wordmark" /> AWS</span><small>AWS adapter</small></div>
  </div>
  <div class="shared-effort">
    <p v-click="[1, 2]" class="joined-forces">So we joined forces.</p>
    <div v-click="2">
    <svg viewBox="0 0 840 56" aria-hidden="true"><path d="M140 0v20h560V0M420 0v50m-6-7 6 7 6-7" /></svg>
    <div class="opennext-name"><img src="/opennext.svg" alt="OpenNext" /></div>
    </div>
  </div>
  <p v-click="3" class="collaboration-line">Collaborate. Compare notes. Reuse code. Advocate with one voice.</p>
  <div v-click="4" class="collaboration-question">
    <p class="ambitious-label">More ambitious goal:</p>
    <div class="ambitious-callout">
      <svg viewBox="0 0 24 24" aria-hidden="true"><path d="M5 4h14a2 2 0 0 1 2 2v10a2 2 0 0 1-2 2H9l-5 3v-3a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2Z" /></svg>
      <span>Could we work with the Next.js team at Vercel to improve all this for everyone?</span>
    </div>
  </div>
</div>

<style>
.opennext-collaboration { margin-top: 22px; text-align: center; }
.adapter-teams { display: grid; grid-template-columns: repeat(3, 1fr); gap: 24px; }
.adapter-teams > div { display: flex; flex-direction: column; gap: 10px; }
.adapter-teams span { font-size: 32px; }
.team-brand { display: flex; align-items: center; justify-content: center; gap: 12px; height: 48px; }
.team-brand img { width: 36px; height: 36px; object-fit: contain; }
.team-brand .opennext-wordmark { width: 160px; height: auto; filter: brightness(0) invert(1); }
.adapter-teams small { font-size: 24px; color: #cbd5e1; }
.shared-effort { position: relative; }
.joined-forces { position: absolute; inset: 48px 0 auto; margin: 0; font-size: 30px; }
.shared-effort svg { width: 100%; height: 44px; margin-top: 10px; fill: none; stroke: #94a3b8; stroke-width: 1.5; stroke-linecap: round; stroke-linejoin: round; }
.opennext-name { font-size: 40px; line-height: 1.2; color: #bef264; }
.opennext-name img { display: block; width: 240px; height: 48px; object-fit: contain; margin: 0 auto; filter: brightness(0) invert(1); }
.collaboration-line { margin: 16px 0 0; }
.collaboration-question { margin: 18px 0 0; }
.ambitious-label { margin: 0 0 10px; }
.ambitious-callout { display: flex; align-items: center; gap: 14px; width: 800px; margin: 0 auto; padding: 10px 20px; border: 1.5px solid #94a3b8; border-radius: 24px; background: #17202e; font-size: 26px; line-height: 1.3; text-align: left; }
.ambitious-callout svg { width: 28px; height: 28px; flex-shrink: 0; fill: none; stroke: #cbd5e1; stroke-width: 1.5; stroke-linejoin: round; }
</style>

<!--
- OpenNext began with AWS.
- Shared umbrella; still separate adapters.
-->

---
level: 2
class: authored
clicks: 4
---

# We started with the problems.

<div class="challenge-story">
  <p>We all shared our challenges deploying Next.js.</p>
  <div class="challenge-documents">
    <div class="challenge-document">
      <svg viewBox="0 0 48 56" aria-hidden="true"><path d="M8 2h22l10 10v42H8ZM30 2v12h10M15 24h18M15 32h18M15 40h12" /></svg>
      <span>Netlify</span><small>Deployment challenges</small>
    </div>
    <div v-click="1" class="challenge-document">
      <svg viewBox="0 0 48 56" aria-hidden="true"><path d="M8 2h22l10 10v42H8ZM30 2v12h10M15 24h18M15 32h18M15 40h12" /></svg>
      <span>Cloudflare</span><small>Deployment challenges</small>
    </div>
    <div v-click="2" class="challenge-document">
      <svg viewBox="0 0 48 56" aria-hidden="true"><path d="M8 2h22l10 10v42H8ZM30 2v12h10M15 24h18M15 32h18M15 40h12" /></svg>
      <span>OpenNext AWS</span><small>Deployment challenges</small>
    </div>
  </div>
  <div v-click="3" class="jimmy-conversation">
    <img src="/nextjs.svg" alt="" />
    <div>We talked with Jimmy Lai.<small>Leading the Next.js team at Vercel</small></div>
  </div>
  <p v-click="4" class="jimmy-partner">He became a wonderful trusted partner for all of us.</p>
</div>

<style>
h1 { margin-bottom: 24px !important; }
.challenge-story > p { margin: 0; }
.challenge-documents { display: grid; grid-template-columns: repeat(3, 1fr); gap: 24px; margin: 28px 0; }
.challenge-document { display: flex; flex-direction: column; align-items: center; gap: 8px; }
.challenge-document svg { width: 48px; height: 56px; fill: none; stroke: #94a3b8; stroke-width: 1.5; stroke-linejoin: round; }
.challenge-document span { font-size: 30px; }
.challenge-document small { font-size: 24px; color: #cbd5e1; }
.jimmy-conversation { display: flex; justify-content: center; align-items: center; gap: 20px; margin-top: 32px; font-size: 30px; }
.jimmy-conversation img { width: 48px; height: 48px; filter: brightness(0) invert(1); }
.jimmy-conversation small { display: block; font-size: 24px; color: #cbd5e1; }
.challenge-story .jimmy-partner { margin-top: 24px; text-align: center; }
</style>

<!--
- Jimmy Lai.
- Real constraints → trusted engineering partner.
-->

---
level: 2
class: authored
---

# It worked. We drafted an adapter RFC together.

<p class="rfc-intro">It became obvious what the solution was to many of our challenges...</p>

<a v-click="1" href="https://github.com/vercel/next.js/discussions/77740" target="_blank" class="rfc-screenshot">
  <img src="/next-adapter-rfc.png" alt="April 2, 2025: Next.js RFC for a Deployment Adapters API. Vercel will use the same adapter API as every other partner." />
</a>

<style>
h1 { margin-bottom: 24px !important; }
.rfc-screenshot { display: block; width: 850px; margin: 0 auto; border: 0 !important; }
.rfc-screenshot img { width: 100%; border-radius: 8px; }
.rfc-intro { margin: 0 0 20px; font-size: 26px; line-height: 1.4; }
</style>

<!--
- Public RFC: April 2, 2025.
-->

---
level: 2
class: authored
clicks: 3
---

# We kept meeting. And the group grew.

<div class="working-group-name">Next.js Deployment Adapters<br />Working Group</div>

<div class="working-group-members">
  <span><img src="/nextjs.svg" alt="" class="white-logo" />Next.js / Vercel</span>
  <span><img src="/netlify.svg" alt="" />Netlify</span>
  <span><img src="/cloudflare.svg" alt="" />Cloudflare</span>
  <span><img src="/opennext.svg" alt="OpenNext" class="wg-opennext white-logo" />AWS</span>
  <span v-click="1" class="joining-member google-member"><span class="google-logos"><img src="/google-cloud.svg" alt="" /><img src="/firebase.svg" alt="" /></span>Google Cloud / Firebase</span>
  <span v-click="2" class="joining-member"><img src="/aws-amplify.svg" alt="" />AWS Amplify</span>
</div>

<div class="working-group-work">
  <p v-click="3">Bring feedback. Ideate. Iterate.</p>
</div>

<style>
.working-group-name { margin-top: 28px; font-size: 36px; line-height: 1.3; text-align: center; }
.working-group-members { display: grid; grid-template-columns: repeat(3, 1fr); gap: 22px 18px; margin: 36px 0; text-align: center; font-size: 26px; }
.working-group-members > span { display: flex; align-items: center; justify-content: center; gap: 10px; padding-bottom: 10px; border-bottom: 1px solid #475569; }
.working-group-members img { width: 32px; height: 32px; object-fit: contain; }
.working-group-members .wg-opennext { width: 150px; height: auto; }
.white-logo { filter: brightness(0) invert(1); }
.working-group-members .google-member { flex-direction: column; gap: 6px; font-size: 24px; }
.google-logos { display: flex; gap: 10px; }
.joining-member { color: #bef264; }
.working-group-work p { margin: 18px 0 0; }
</style>

<!--
- Biweekly calls; months of feedback.
- Google Cloud, then AWS Amplify.
- OpenNext AWS ≠ AWS Amplify.
-->

---
level: 2
class: authored
clicks: 4
---

# Then we had to make it work.

<div class="adapter-feedback-loop">
  <div>Vercel implemented<br />the API and its adapter.</div>
  <svg v-click="1" viewBox="0 0 60 32" aria-hidden="true"><path d="M4 16h48m-8-7 8 7-8 7" /></svg>
  <div v-click="1">We built prototypes<br />for our platforms.</div>
  <svg v-click="2" class="feedback-return" viewBox="0 0 780 70" aria-hidden="true"><path d="M600 3v35Q600 55 580 55H200Q180 55 180 35V3m-7 9 7-9 7 9" /></svg>
  <span v-click="2" class="feedback-caption">More feedback. Fixes. Another round.</span>
</div>

<div class="adapter-release-milestones">
  <div v-click="3"><span class="release-version">Next.js 16</span><span class="release-state">Alpha</span><small>October 2025</small></div>
  <svg v-click="4" viewBox="0 0 80 32" aria-hidden="true"><path d="M4 16h68m-8-7 8 7-8 7" /></svg>
  <div v-click="4"><span class="release-version">Next.js 16.2</span><span class="release-state stable">Stable</span><small>March 2026</small></div>
</div>

<style>
.adapter-feedback-loop { position: relative; display: grid; grid-template-columns: 1fr 60px 1fr; align-items: center; width: 780px; margin: 40px auto 0; padding-bottom: 110px; }
.adapter-feedback-loop > div { text-align: center; font-size: 28px; line-height: 1.4; }
.adapter-feedback-loop svg, .adapter-release-milestones svg { fill: none; stroke: #94a3b8; stroke-width: 1.5; stroke-linecap: round; stroke-linejoin: round; }
.adapter-feedback-loop > svg:not(.feedback-return) { width: 60px; height: 32px; }
.feedback-return { position: absolute; top: 86px; left: 0; width: 780px; height: 70px; }
.feedback-caption { position: absolute; left: 0; right: 0; bottom: 0; text-align: center; color: #cbd5e1; }
.adapter-release-milestones { display: flex; align-items: center; justify-content: center; gap: 40px; margin-top: 42px; }
.adapter-release-milestones > div { display: grid; grid-template-columns: auto auto; align-items: center; gap: 10px 18px; }
.release-version { font-size: 32px; }
.release-state { color: #cbd5e1; border-bottom: 2px solid #94a3b8; }
.release-state.stable { color: #bef264; border-color: #bef264; }
.adapter-release-milestones small { grid-column: 1 / -1; font-size: 24px; color: #cbd5e1; }
.adapter-release-milestones svg { width: 80px; height: 32px; }
</style>

<!--
- Prototypes → feedback → implementation changes.
- Stable API ≠ every adapter shipped.
-->

---
level: 2
class: authored
clicks: 3
title: Dogfooded on Vercel first
---

<h1><DogfoodWord /> on Vercel first</h1>

<p class="dogfooding-intro">They rebuilt their own Next.js integration first.</p>

<div class="vercel-rebuild">
  <div class="old-integration">
    <div class="integration-label">Before</div>
    <div class="integration-box"><div><span class="private-accent">Private</span> code paths<br />inside Next.js</div></div>
    <span class="integration-plus">+</span>
    <div class="integration-box"><div><span class="private-accent">Closed-source</span> integration<br />inside Vercel's platform</div></div>
  </div>
  <svg v-click="1" class="replacement-arrow" viewBox="0 0 64 32" aria-hidden="true"><path d="M4 16h52m-8-7 8 7-8 7" /></svg>
  <div v-click="1" class="new-integration">
    <div class="integration-label">Now</div>
    <div class="integration-box"><div><span class="public-accent">Public</span> deployment adapter <span class="public-accent">API</span><br />inside Next.js</div></div>
    <svg class="adapter-down" viewBox="0 0 32 36" aria-hidden="true"><path d="M16 2v28m-6-7 6 7 6-7" /></svg>
    <div class="integration-box open-adapter">Vercel's deployment adapter<small>Open source</small></div>
  </div>
</div>

<div class="contract-outcome">
  <p v-click="2">Next.js on Vercel now powered by an open-source adapter using the same public API as everyone else.</p>
  <p v-click="3">Also serves as a reference implementation.</p>
</div>

<style>
h1 { margin-bottom: 38px !important; }
.dogfooding-intro { margin: 0; font-size: 28px; }
.vercel-rebuild { display: grid; grid-template-columns: 1fr 64px 1fr; align-items: center; gap: 20px; margin: 24px 0; text-align: center; }
.integration-label { margin-bottom: 12px; color: #cbd5e1; }
.integration-box { display: flex; min-height: 82px; flex-direction: column; justify-content: center; padding: 10px 14px; border: 1.5px solid #94a3b8; border-radius: 10px; background: #17202e; line-height: 1.3; }
.integration-plus { display: block; height: 36px; color: #94a3b8; }
.vercel-rebuild svg { fill: none; stroke: #94a3b8; stroke-width: 1.5; stroke-linecap: round; stroke-linejoin: round; }
.replacement-arrow { width: 64px; height: 32px; }
.adapter-down { display: block; width: 32px; height: 36px; margin: 0 auto; }
.open-adapter small { font-size: 24px; color: #bef264; }
.private-accent { color: #fdba74; }
.public-accent { color: #bef264; }
.contract-outcome p { margin: 14px 0 0; }
</style>

<!--
- Credit Vercel: rebuilt its own integration against the same public API.
- Private mode + platform internals → open-source adapter.
-->

---
level: 2
class: authored
clicks: 5
---

# Adapters roadmap

<div class="adapter-status-list">
  <div><span class="status-platform">Vercel</span><span>Open source. Used on Vercel.</span></div>
  <div v-click="1"><span class="status-platform">Kubernetes</span><span>Very soon. By James Daniels (formerly Google).</span></div>
  <div v-click="2"><span class="status-platform">Netlify</span><span>New adapter in development.</span></div>
  <div v-click="3"><span class="status-platform">Cloudflare</span><span>New adapter in development.</span></div>
  <div v-click="4"><span class="status-platform">OpenNext AWS</span><span>New adapter in development.</span></div>
  <div v-click="5" class="redacted-row">
    <span class="redacted-platform"><span v-if="$clicks >= 5" class="redacted-stamp">REDACTED</span></span>
    <span>New adapter in development.</span>
  </div>
</div>

<style>
.adapter-status-list { margin-top: 16px; }
.adapter-status-list > div { display: grid; grid-template-columns: 290px 1fr; gap: 20px; align-items: center; padding: 8px 0; border-bottom: 1px solid #475569; }
.status-platform { font-size: 28px; }
.adapter-status-list > div > span:last-child { color: #cbd5e1; }
.adapter-status-list > .redacted-row { min-height: 76px; }
.redacted-platform { display: flex; align-items: center; }
.adapter-status-list .redacted-stamp { display: inline-block; padding: 3px 10px; border: 4px double #f87171; color: #f87171; font-family: var(--slidev-code-font-family); font-size: 24px; font-weight: 900; letter-spacing: .12em; line-height: 1.1; transform: rotate(-5deg); animation: redacted-slam 500ms cubic-bezier(.16, 1, .3, 1) both; }
@keyframes redacted-slam {
  0% { opacity: 0; transform: scale(1.8) rotate(-14deg); }
  65% { opacity: 1; transform: scale(.95) rotate(-4deg); }
  100% { transform: scale(1) rotate(-5deg); }
}
@media (prefers-reduced-motion: reduce) { .adapter-status-list .redacted-stamp { animation: none; } }
</style>

<!--
- New API adapters; existing Next.js deployments already work.
- Kubernetes: James Daniels, formerly Google.
-->

---
level: 2
class: authored
clicks: 2
---

# And we kept talking.

<div class="ecosystem-transition">
  <div class="former-group">Next.js Deployment Adapters Working Group</div>
  <div v-click="1">
    <svg class="group-arrow" viewBox="0 0 32 52" aria-hidden="true"><path d="M16 2v42m-7-8 7 8 7-8" /></svg>
    <div class="successor-group">Next.js Ecosystem Working Group</div>
  </div>
  <p v-click="2">The collaboration grew beyond adapters.</p>
</div>

<style>
.ecosystem-transition { margin-top: 58px; text-align: center; }
.former-group { color: #cbd5e1; font-size: 28px; }
.group-arrow { width: 32px; height: 52px; margin: 18px auto; fill: none; stroke: #94a3b8; stroke-width: 1.5; stroke-linecap: round; stroke-linejoin: round; }
.successor-group { font-size: 36px; color: #bef264; }
.ecosystem-transition p { margin: 32px 0 0; font-size: 28px; }
</style>

<!--
- Canary feedback, security coordination, core-team PRs to our adapter.
- Relationships outlasted the adapter project.
-->

---
level: 2
layout: center
class: authored co-op-slide
title: Co-op mode
clicks: 2
---

<div class="co-op-interstitial">
  <LevelProgress :level="$clicks >= 1 ? 8 : 7" />
  <CoopPlayers :active="$clicks >= 1" />
  <p v-click="2">Meanwhile, we’ve been grinding through other campaigns…</p>
</div>

<style>
.co-op-interstitial { display: flex; flex-direction: column; align-items: center; }
.co-op-interstitial :deep(.level-badge) { margin: 0; }
.co-op-interstitial :deep(.level-number) { display: flex; align-items: center; padding: 14px 18px; font-size: 24px; }
.co-op-interstitial :deep(.level-title) { display: flex; align-items: center; padding: 14px 22px; font-size: 30px; white-space: pre; }
.co-op-interstitial p { position: relative; top: 24px; margin: 44px 0 0; font-size: 32px; }
</style>

<!--
- Next.js was one framework. Zoom back out.
-->
