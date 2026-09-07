---
layout: center
class: authored reality-interstitial
hideInToc: true
---

<div class="reality-line">Press pause on ZurichCloud for a moment.<br />Back to reality.</div>

<style>
.reality-line { font-size: 44px; line-height: 1.4; text-align: center; color: #a5f3fc; }
</style>

<!--
Pause the ZurichCloud role play here. The next slides tell the real story of the teams working together on Next.js deployment support.
-->

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
About 35 seconds. This is where we leave the fictional platform and tell the real collaboration story.

Start: three teams were solving similar deployment problems for different infrastructure. OpenNext started with the AWS adapter; Netlify and Cloudflare later joined the broader effort.

Click 1: So we joined forces.
Click 2: OpenNext became the umbrella. These remain separate adapters, not one shared implementation. The connecting lines represent collaboration, not build output.
Click 3: share findings and fixes where possible, compare the things we keep having to reverse-engineer, and advocate together.
Click 4: transition from maintaining workarounds to working with the framework team on a supported contract.

Source: https://opennext.js.org/ (checked 2026-09-06). Its overview describes the AWS origins, the three adapters, and the joint deployment API effort.
The first-person collaboration story comes from Philippe's talk notes in this conversation.
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
Tell the collaboration story at its own pace; trim after rehearsing the complete deck.

Start: we put together a document of the challenges making Next.js work on Netlify. We went through the integration, its hacks and assumptions, and the things we needed from the framework.
Clicks 1–2: Cloudflare did the same, and so did OpenNext AWS. The document icons are schematic, not reproductions of their actual documents.
Click 3: we discussed this with Jimmy Lai, who was leading the Next.js team at Vercel. Use his name, not the speech transcription "Jimmy Lay". This role and the conversations are Philippe's firsthand account, not a claim about Jimmy's present title.
Click 4: Jimmy became a great partner. This was a constructive engineering conversation about real constraints, not just asking a competitor to fix our problems.

The personal sequence and assessment of the partnership come from Philippe's account in this conversation. The Next.js retrospective also quotes Philippe about compiling the integration problems and identifying the missing stable contract.

Sources, checked 2026-09-07:
https://github.com/vercel/next.js/discussions/77740
https://nextjs.org/blog/nextjs-across-platforms
https://nextjs.org/blog/next-16 (Jimmy Lai's name)
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
The original public RFC announcement, April 2, 2025. The live discussion has since been updated. Screenshot supplied by Philippe.

The proposal grew out of the concrete deployment challenges we shared with the Next.js team.
Source: https://github.com/vercel/next.js/discussions/77740
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
We started meeting regularly and called this the Next.js Deployment Adapters Working Group. We had bi-weekly calls, alongside ongoing conversations on Discord and GitHub.

Clicks 1–2: we brought in the Google Cloud team, then AWS Amplify. This order is Philippe's firsthand account; don't conflate the community's OpenNext AWS adapter with the AWS Amplify team.
Click 3: we compared the proposed spec with the workarounds in our existing integrations. What would it solve? What would still require reaching into internals? We shared detailed feedback, revised the design, and repeated that process over several months.
Save the collaboration beyond adapters and the transition to the Ecosystem Working Group for the final slide of this section.

Sources, checked 2026-09-07:
https://www.netlify.com/blog/the-next-js-adapter-api-just-shipped-here-s-what-comes-next/ (Philippe's March 2026 account: bi-weekly calls, growing group, security and release coordination)
https://firebase.blog/posts/2026/03/nextjs-adapters/ (James Daniels's account of the working group)
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
Start: the Next.js team implemented the API and Vercel built its own adapter. They used it internally and learned from real deployments.
Click 1: Netlify, Cloudflare, OpenNext AWS, and Google Cloud started prototypes of their integrations against the new API. These were spikes, not simultaneous production releases.
Click 2: implementation exposed more issues. We gave feedback on the actual behavior, they fixed bugs and refined the API, and we tried again. This loop continued through the alpha period; the arrows aren't a strict chronology where all feedback preceded alpha.
Click 3: the API shipped as alpha in Next.js 16, October 2025. It was already included in the Next.js 16 beta; don't imply the final 16.0 release was its first appearance anywhere.
Click 4: stable in Next.js 16.2, March 2026. Stable API does not mean every platform's new adapter had shipped.

Sources, checked 2026-09-07:
https://nextjs.org/blog/next-16 (Build Adapters API alpha)
https://nextjs.org/blog/next-16-2 (Adapters stable)
https://www.netlify.com/blog/the-next-js-adapter-api-just-shipped-here-s-what-comes-next/ (Vercel dogfooding and platform implementation work)
Prototype and feedback details also come from Philippe's firsthand account.
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
The important decision was to adopt the API for Vercel's own platform, not merely offer it to other platforms. Give Vercel explicit credit for making that commitment and doing the work.

Start: previously the integration was split between private Next.js code paths (including minimal mode) and implementation inside Vercel's closed-source platform. Connect this to the minimal-mode snippet and dog from the earlier slide.
Click 1: Vercel rebuilt that integration as an open-source Next.js deployment adapter using the public API. The platform itself remains proprietary; the diagram is about the Next.js integration boundary, not open-sourcing Vercel's infrastructure.
Click 2: one inspectable adapter against the same contract we use. Dogfooding means real requirements from Vercel's deployments exercise that API too. The significance is the deliberate architectural choice, not just another adapter in the list.
The integration Vercel uses is also a reference implementation other platform teams can read and learn from. Don't claim every existing Vercel project has migrated; the exact rollout percentage isn't established here.

Technical context if useful aloud: the stable contract provides documented, typed build output; breaking changes require a Next.js major. A shared upstream end-to-end test suite is available to adapter authors. These details support the story, but the main point on this slide is Vercel's choice to use the public API themselves.

Sources:
https://nextjs.org/blog/nextjs-across-platforms (March 25, 2026: stable contract, Vercel's public implementation, breaking-change policy)
https://nextjs.org/blog/next-16-2
https://opennext.js.org/
https://www.netlify.com/blog/the-next-js-adapter-api-just-shipped-here-s-what-comes-next/ (historical private integration and Vercel adopting the public adapter)
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
Status snapshot checked 2026-09-07. Refresh release status before presenting; these rows describe adapters built on the new official API, not whether Next.js works on those platforms today.

Start: Vercel uses its public adapter. Its precise deployment rollout percentage is not established here.
Click 1: James Daniels's Kubernetes implementation is public at nextjs/adapter-k8s. It grew out of the Google Cloud/GKE work Philippe described. The README says compatibility is verified against the upstream suite, but operational hardening remains; the npm package is not yet published. Say "public implementation," not "production ready" or "GA." Don't discuss its infrastructure in detail here.
Click 2: Netlify and Cloudflare are rebuilding their integrations around the official API. Philippe expects these soon, but public sources don't establish a release date. Existing integrations already serve users. This can unlock implementation and performance improvements as well as removing maintenance work; don't promise a benchmark.
Click 3: reveal Cloudflare separately.
Click 4: the community's OpenNext AWS adapter is also in development against the API. AWS Amplify participated in the design; we haven't verified a public release status for its new implementation, so it isn't assigned one in this table.
Click 5: the REDACTED stamp. Leave the identity unspecified.

Sources:
https://nextjs.org/blog/nextjs-across-platforms
https://github.com/nextjs/adapter-k8s (Status and Quick start)
https://opennext.js.org/
https://www.netlify.com/blog/the-next-js-adapter-api-just-shipped-here-s-what-comes-next/

Logo assets embedded locally: OpenNext wordmark extracted from the header SVG at https://opennext.js.org/; Netlify, Cloudflare, AWS Amplify, Google Cloud and Firebase from https://api.iconify.design/logos/ (respective netlify-icon, cloudflare-icon, aws-amplify, google-cloud, firebase assets).
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
When the API became stable, the Deployment Adapters Working Group wrapped up. The collaboration continued in the broader Next.js Ecosystem Working Group.

Click 1: reveal the successor group. Philippe describes this as the original group disbanding and becoming the Ecosystem WG; the public announcement describes a new permanent forum.
Click 2: the relationships now support more than adapter design: early feedback on upcoming changes, canary issues, and security coordination. Philippe also received contributions from the Next.js core team to Netlify's adapter during the collaboration. The broader forum has public meeting notes and a wider remit.

Sources:
https://nextjs.org/blog/nextjs-across-platforms
https://www.netlify.com/blog/the-next-js-adapter-api-just-shipped-here-s-what-comes-next/
Philippe's firsthand account in this conversation supplies the group's transition and personal collaboration details.
-->
