---
level: 2
class: authored closing-user
clicks: 2
---

# Back to the user.

<div class="closing-request">
  <img src="/patak-cat.png" alt="The developer" />
  <div>I just want to deploy my site.</div>
</div>

<div v-click="1" class="closing-choices">
  <div>
    <span>The framework they want.</span>
    <div class="choice-logos">
      <img src="/astro.svg" alt="Astro" class="closing-mono" />
      <img src="/svelte.svg" alt="SvelteKit" class="closing-mono" />
      <img src="/tanstack.svg" alt="TanStack Start" />
      <img src="/nextjs.svg" alt="Next.js" class="closing-mono" />
      <span>…</span>
    </div>
  </div>
  <span class="choice-plus">+</span>
  <div>
    <span>The platform they want.</span>
    <div class="choice-logos">
      <img src="/netlify.svg" alt="Netlify" />
      <img src="/cloudflare.svg" alt="Cloudflare" />
      <img src="/fetchable/vercel.svg" alt="Vercel" class="closing-mono" />
      <img src="/zurich-cloud-symbol.svg" alt="ZurichCloud" />
      <span>…</span>
    </div>
  </div>
</div>

<p v-click="2" class="closing-responsibility">Let's make it easy and boring for them.<br />And sustainable for us.</p>

<style>
.closing-user .closing-request { display: flex; align-items: center; gap: 30px; margin: 30px 0; }
.closing-request > img { width: 100px; height: 100px; object-fit: cover; border-radius: 50%; }
.closing-request > div { position: relative; border: 1px solid #64748b; border-radius: 12px; padding: 20px 28px; font-size: 34px; background: #17202e; }
.closing-request > div::before { content: ''; position: absolute; left: -8px; top: 35px; width: 14px; height: 14px; background: #17202e; border-left: 1px solid #64748b; border-bottom: 1px solid #64748b; transform: rotate(45deg); }
.closing-choices { display: grid; grid-template-columns: 1fr 48px 1fr; align-items: center; gap: 18px; margin-top: 26px; }
.closing-choices > div { padding: 20px; border-top: 1px solid #64748b; border-bottom: 1px solid #64748b; font-size: 27px; }
.choice-logos { display: flex; align-items: center; justify-content: space-between; margin-top: 20px; }
.choice-logos img { width: 39px; height: 39px; object-fit: contain; }
.choice-logos > span { font-size: 32px; color: #94a3b8; }
.choice-plus { text-align: center; color: #94a3b8; font-size: 36px; }
.closing-mono { filter: brightness(0) invert(1); }
.closing-user .closing-responsibility { margin-top: 32px; font-size: 29px; line-height: 1.35; color: #bef264; }
</style>

<!--
- Choice without waiting for every framework × platform integration.
- Collaboration is how we make that sustainable.
-->

---
level: 2
class: authored closing-coop
---

# Thanks!

<div class="closing-netlify"><img src="/netlify-full.svg" alt="Netlify" /></div>

<div class="closing-finale">
  <div class="closing-invitation">
    <LevelBadge :number="8">Frontend cloud, co-op mode</LevelBadge>
    <CoopPlayers active />
    <p>Bring your framework.<br />Bring your platform.</p>
  </div>
  <div class="closing-resources">
    <a href="https://www.netlify.com/blog/the-next-js-adapter-api-just-shipped-here-s-what-comes-next/">Deep dive on deploying Next.js</a>
    <a href="https://fetchable.org">fetchable.org</a>
    <a href="https://github.com/vitejs/vite/discussions/20907">The Vite discussion</a>
    <a href="https://github.com/vitejs/deployment-metadata">vitejs/deployment-metadata</a>
  </div>
</div>

<div class="closing-contact">
  <strong>Philippe Serhal</strong>
  <span class="closing-social-pair"><a href="https://bsky.app/profile/philippeserhal.com"><img src="/bluesky.svg" alt="Bluesky" /></a><a href="https://tangled.org/philippeserhal.com"><img src="/tangled.svg" alt="Tangled" />@philippeserhal.com</a></span>
  <span class="closing-social-pair"><img src="/discord.svg" alt="Discord" /><a href="https://github.com/serhalp"><img src="/github.svg" alt="GitHub" />@serhalp</a></span>
</div>

<style>
.closing-netlify { position: absolute; top: 36px; right: 56px; }
.closing-netlify img { width: 190px; height: auto; }
.closing-finale { display: grid; grid-template-columns: 1.15fr 1fr; gap: 48px; align-items: start; margin-top: 40px; }
.closing-invitation :deep(.level-title) { font-size: 15px; white-space: nowrap; padding: 10px; }
.closing-invitation :deep(.level-number) { font-size: 15px; white-space: nowrap; padding: 10px; }
.closing-invitation .co-op-players { margin: 24px 0 16px; gap: 12px; justify-content: flex-start; }
.closing-invitation :deep(.player) { width: 48px; }
.closing-coop .closing-invitation p { font-size: 30px; line-height: 1.5; margin: 20px 0 0; }
.closing-resources { display: flex; flex-direction: column; gap: 18px; padding-left: 26px; border-left: 1px solid #475569; }
.closing-resources a { width: fit-content; font-size: 25px; line-height: 1.3; }
.closing-resources span { display: block; margin-top: 5px; font-size: 20px; color: #cbd5e1; }
.closing-contact { position: absolute; bottom: 35px; left: 56px; right: 56px; display: flex; align-items: center; justify-content: space-between; gap: 20px; padding-top: 20px; border-top: 1px solid #475569; font-size: 23px; }
.closing-contact strong { font-size: 26px; font-weight: 400; }
.closing-contact a { display: flex; align-items: center; gap: 8px; border-bottom: none !important; text-decoration: none !important; }
.closing-social-pair { display: flex; align-items: center; gap: 8px; }
.closing-contact img { width: 23px; height: 23px; object-fit: contain; filter: brightness(0) invert(1); }
</style>

<!--
- Thank the collaborators; invite more frameworks and platforms.
-->
