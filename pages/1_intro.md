---
layout: default
class: cover-intro
hideInToc: true
clicks: 1
---

<div class="conference-tag"><span>ZurichJS Conf</span><span>2026</span></div>
<img class="cover-netlify" src="/netlify-full.svg" alt="Netlify" />

<div class="cover-titles" :class="{ 'alternate-shown': $clicks >= 1 }">
<h1 class="cover-title">
  <span>How to make</span>
  <span class="cover-emphasis">full-stack frameworks</span>
  <span>work on a platform</span>
  <span>like Netlify</span>
</h1>
<div class="cover-alternate">
  <em>or…</em>
  <div>So you want to build<br /><span>a frontend cloud</span></div>
</div>
</div>

<div class="cover-footer">
  <div class="speaker-card">
    <div class="speaker-name">Philippe Serhal</div>
    <div class="speaker-role">Staff Engineer @ Netlify</div>
    <div class="speaker-socials">
      <span class="shared-social-handle"><a href="https://bsky.app/profile/philippeserhal.com"><img src="/bluesky.svg" alt="Bluesky"></a><a href="https://tangled.org/philippeserhal.com"><img src="/tangled.svg" alt="Tangled">@philippeserhal.com</a></span>
      <img src="/discord.svg" alt="Discord" />
      <a class="github-social" href="https://github.com/serhalp"><img src="/github.svg" alt="GitHub">@serhalp</a>
    </div>
  </div>
  <div class="speaker-affiliations">
    <div><img src="/npmx.svg" alt=""><span><strong>npmx</strong> core team</span></div>
    <div><img src="/vite.svg" alt=""><span><strong>Vite</strong> team advisor</span></div>
    <div><img class="monochrome-logo" src="/nextjs.svg" alt=""><span><strong>Next.js</strong> Ecosystem Working Group member</span></div>
  </div>
</div>

---
hideInToc: true
class: authored talk-overview
---

# Here's the plan.

<div class="talk-plan">
  <div><span class="plan-number">01</span><span>Build a frontend cloud.</span><img src="/zurich-cloud-symbol.svg" alt="ZurichCloud" /></div>
  <div><span class="plan-number">02</span><span>Get <em>all</em> the frameworks working on it.</span><div class="plan-logos"><img class="plan-mono" src="/astro.svg" alt="Astro" /><img class="plan-mono" src="/svelte.svg" alt="SvelteKit" /></div></div>
  <div><span class="plan-number">03</span><span>Work together to make it better.</span><div class="plan-logos"><img src="/netlify.svg" alt="Netlify" /><img src="/cloudflare.svg" alt="Cloudflare" /><img src="/vite.svg" alt="Vite" /></div></div>
</div>

<style>
.talk-plan { display: flex; flex-direction: column; margin-top: 50px; }
.talk-plan > div { display: grid; grid-template-columns: 58px 1fr 146px; align-items: center; gap: 20px; min-height: 102px; border-bottom: 1px solid #475569; font-size: 32px; }
.talk-plan > div:first-child { border-top: 1px solid #475569; }
.plan-number { font-family: var(--slidev-code-font-family); font-size: 23px; color: #bef264; }
.talk-plan img { width: 38px; height: 38px; object-fit: contain; }
.talk-plan > div > img { justify-self: end; }
.plan-logos { display: flex; justify-content: flex-end; align-items: center; gap: 16px; }
.plan-logos .plan-mono { filter: brightness(0) invert(1); }
</style>
