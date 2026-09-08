---
level: 2
class: authored
---

# ZurichCloud enters the server-rendering era

<LevelBadge :number="5">Full stack</LevelBadge>

<div class="ssr-premise">The user wants to render pages at request time.</div>

<div v-click="1" class="ssr-frameworks">
  <div><strong>Server-side rendering (SSR)</strong></div>
  <ToolLogos :revealed="$clicks >= 1" :logos="[
    { name: 'Next.js', src: '/nextjs.svg' },
    { name: 'Nuxt', src: '/nuxt.svg' },
    { name: 'SvelteKit', src: '/svelte.svg' },
    { name: 'Astro', src: '/astro.svg' },
    { name: 'React Router', src: '/reactrouter.svg' },
  ]" />
</div>

<svg v-click="2" viewBox="0 0 868 174" class="ssr-flow" role="img" aria-label="A cat represents the visitor using a browser to request hello.zurich.cloud/about. A ZurichCloud server calls Astro and returns the rendered About page.">
  <image href="/patak-cat.png" x="2" y="48" width="78" height="78"><title>patak's cat, the visitor</title></image>
  <text x="41" y="151" text-anchor="middle" fill="#cbd5e1" style="font-size: 18px">Visitor</text>
  <rect x="104" y="5" width="336" height="164" rx="12" fill="#17202e" stroke="#94a3b8" stroke-width="2" />
  <path d="M104 48 H440" stroke="#94a3b8" stroke-width="2" />
  <text x="120" y="34" fill="#e2e8f0" font-family="monospace" style="font-size: 18px">hello.zurich.cloud/<tspan fill="#f0abfc">about</tspan></text>
  <text x="124" y="88" fill="#f1f5f9" style="font-size: 28px">About</text>
  <text x="124" y="120" fill="#cbd5e1" style="font-size: 22px">Hello from Zurich.</text>
  <path d="M124 139 H411 M124 151 H340" stroke="#64748b" stroke-width="3" stroke-linecap="round" />

  <path d="M456 72 H578 m-10 -7 10 7 -10 7" fill="none" stroke="#67e8f9" stroke-width="2" />
  <text x="517" y="57" text-anchor="middle" fill="#67e8f9" style="font-size: 20px">Request</text>
  <path d="M578 126 H456 m10 -7 -10 7 10 7" fill="none" stroke="#cbd5e1" stroke-width="2" />
  <text x="517" y="153" text-anchor="middle" fill="#cbd5e1" style="font-size: 20px">HTML</text>

  <rect x="594" y="5" width="272" height="164" rx="12" fill="#1b2416" stroke="#bef264" stroke-width="2" />
  <image href="/zurich-cloud.svg" x="609" y="20" width="142" height="22"><title>ZurichCloud</title></image>
  <text x="851" y="37" text-anchor="end" fill="#cbd5e1" style="font-size: 18px">Server</text>
  <rect x="614" y="60" width="232" height="90" rx="8" fill="#132a32" stroke="#67e8f9" stroke-width="2" />
  <image href="/astro.svg" x="634" y="73" width="34" height="28" style="filter: brightness(0) invert(1)" />
  <text x="682" y="96" fill="#e2e8f0" style="font-size: 24px">Astro</text>
  <text x="730" y="132" text-anchor="middle" fill="#67e8f9" font-family="monospace" style="font-size: 20px">render(request)</text>
</svg>

<style>
h1 { margin-bottom: 12px !important; }
h2 { margin-bottom: 20px !important; }
.ssr-premise { margin-bottom: 32px; }
.ssr-frameworks :deep(.tool-logo) { font-size: 22px; }
.ssr-flow { display: block; width: 100%; height: 174px; margin-top: 24px; }
</style>

<!--
- SSR = render when a request arrives.
- render(request) is still our toy example.
-->

---
class: authored
---

# Introducing ZurichCloud Functions

<LevelBadge :number="5">Full stack</LevelBadge>

<!-- prettier-ignore -->
```ts [.zurich/hello.ts]
export default async (request: Request) =>
  new Response("Hello world!");

export const config = {
  path: "/functions/hello",
};
```

<svg v-click="1" class="mt-7" viewBox="0 0 868 142" role="img" aria-label="A visitor requests /functions/hello. ZurichCloud calls hello.ts and returns Hello world.">
  <image href="/patak-cat.png" x="0" y="38" width="64" height="64" />
  <text x="32" y="127" text-anchor="middle" fill="#cbd5e1" style="font-size: 18px">Visitor</text>
  <rect x="82" y="3" width="430" height="136" rx="12" fill="#17202e" stroke="#64748b" stroke-width="2" />
  <path d="M82 47H512" stroke="#64748b" />
  <text x="96" y="32" fill="#e2e8f0" font-family="monospace" style="font-size: 17px">hello.zurich.cloud/<tspan fill="#f0abfc">functions/hello</tspan></text>
  <text v-click="2" x="106" y="99" fill="#f8fafc" style="font-size: 28px">Hello world!</text>
  <path d="M528 51H606l-9 -6m9 6l-9 6" fill="none" stroke="#67e8f9" stroke-width="2" />
  <text x="567" y="32" text-anchor="middle" fill="#67e8f9" style="font-size: 18px">Request</text>
  <g v-click="2">
    <path d="M606 104H528l9 -6m-9 6l9 6" fill="none" stroke="#cbd5e1" stroke-width="2" />
    <text x="567" y="132" text-anchor="middle" fill="#cbd5e1" style="font-size: 18px">Response</text>
  </g>
  <rect x="622" y="3" width="244" height="136" rx="12" fill="#1b2416" stroke="#bef264" stroke-width="2" />
  <image href="/zurich-cloud.svg" x="642" y="18" width="148" height="24" />
  <rect x="642" y="59" width="204" height="58" rx="8" fill="#132a32" stroke="#67e8f9" />
  <text x="744" y="95" text-anchor="middle" fill="#67e8f9" font-family="monospace" style="font-size: 24px">hello.ts</text>
</svg>

<style>
h1 { margin-bottom: 12px !important; }
</style>

<!--
- Platform runs the code; user doesn’t start a server.
- Function modules aren’t public files.
-->

---
level: 2
class: authored
---

# Run SSR via ZurichCloud Functions

<LevelBadge :number="5">Full stack</LevelBadge>

````md magic-move {at:1} {duration:700}
```ts [.zurich/ssr.ts]
import { render } from "./dist/server/entry.mjs";
```

```ts [.zurich/ssr.ts]
import { render } from "./dist/server/entry.mjs";

export default async (request: Request) => {
  const html = "...";
  return new Response(html, {
    headers: { "Content-Type": "text/html" },
  });
};
```

```ts [.zurich/ssr.ts]
import { render } from "./dist/server/entry.mjs";

export default async (request: Request) => {
  const html = await render(request);
  return new Response(html, {
    headers: { "Content-Type": "text/html" },
  });
};
```

```ts [.zurich/ssr.ts]
import { render } from "./dist/server/entry.mjs";

export default async (request: Request) => {
  const html = await render(request);
  return new Response(html, {
    headers: { "Content-Type": "text/html" },
  });
};

export const config = {
  path: "/*",
};
```
````

<style>
h1 { margin-bottom: 12px !important; }
</style>

<!--
- Generate the wrapper at build time; render at request time.
-->

---
level: 2
class: authored
---

<div class="summary-heading">

# The story so far

<LevelProgress v-click="1" :level="Math.min(Math.max($clicks, 1), 5)" />

</div>

<svg class="mt-5" viewBox="0 0 868 350" role="img" aria-label="One build deploys static assets to the CDN and server code to ZurichCloud Functions. The visitor requests a rendered page from a function, then JavaScript and CSS from the CDN.">
  <defs>
    <marker id="summary-arrow" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="8" markerHeight="8" markerUnits="userSpaceOnUse" orient="auto-start-reverse">
      <path d="M1 1L9 5L1 9" fill="none" stroke="context-stroke" stroke-width="1.7" stroke-linecap="round" stroke-linejoin="round" />
    </marker>
  </defs>
  <g v-click="1">
    <rect x="10" y="115" width="330" height="76" rx="12" fill="#1b2416" stroke="#bef264" stroke-width="2" />
    <image href="/zurich-cloud.svg" x="28" y="128" width="142" height="23" />
    <text x="320" y="149" text-anchor="end" fill="#f8fafc" style="font-size: 24px">CDN</text>
    <text x="175" y="180" text-anchor="middle" fill="#fcd34d" style="font-size: 22px">{{ $clicks < 5 ? "/about.html" : "Static files" }}</text>
  </g>
  <g v-click="2">
    <rect x="30" y="82" width="290" height="25" fill="#111111" />
    <text x="175" y="103" text-anchor="middle" fill="#fcd34d" font-family="monospace" style="font-size: 18px">publish_dir: dist/client/</text>
  </g>
  <g v-click="3">
  <rect x="284" y="1" width="300" height="62" rx="10" fill="#132a32" stroke="#67e8f9" stroke-width="2" />
  <text x="434" y="23" text-anchor="middle" fill="#cbd5e1" font-family="monospace" style="font-size: 18px">build_command</text>
  <text x="434" y="49" text-anchor="middle" fill="#67e8f9" font-family="monospace" style="font-size: 22px">$ astro build</text>
    <path d="M334 63V83H175V87 M175 107V115" fill="none" stroke="#94a3b8" stroke-width="2" />
  </g>
  <g v-click="4" fill="#bef264" font-family="monospace" style="font-size: 18px">
    <rect x="600" y="18" width="110" height="30" rx="8" fill="#202b18" />
    <text x="655" y="39" text-anchor="middle">✨ Auto</text>
    <rect x="334" y="82" width="110" height="30" rx="8" fill="#202b18" />
    <text x="389" y="103" text-anchor="middle">✨ Auto</text>
  </g>
  <g v-click="5">
    <path d="M534 63V83H693V115" fill="none" stroke="#94a3b8" stroke-width="2" />
    <rect x="594" y="82" width="198" height="25" fill="#111111" />
    <text x="693" y="103" text-anchor="middle" fill="#67e8f9" font-family="monospace" style="font-size: 18px">.zurich/ssr.ts</text>
    <rect x="528" y="115" width="330" height="76" rx="12" fill="#1b2416" stroke="#bef264" stroke-width="2" />
    <image href="/zurich-cloud.svg" x="546" y="128" width="142" height="23" />
    <text x="840" y="149" text-anchor="end" fill="#f8fafc" style="font-size: 24px">Functions</text>
    <text x="693" y="180" text-anchor="middle" fill="#67e8f9" font-family="monospace" style="font-size: 22px">render(request)</text>
  </g>
  <g v-click="1">
    <image href="/patak-cat.png" x="212" y="281" width="62" height="62" />
    <rect x="294" y="276" width="400" height="71" rx="10" fill="#17202e" stroke="#64748b" stroke-width="2" />
    <path d="M294 309H694" stroke="#64748b" />
    <text x="310" y="299" fill="#e2e8f0" font-family="monospace" style="font-size: 18px">hello.zurich.cloud/<tspan fill="#f0abfc">about</tspan></text>
    <text x="310" y="335" fill="#f8fafc" style="font-size: 22px">About Zurich</text>
    <g :class="{ 'page-at-function': $clicks >= 5 }" class="page-roundtrip">
      <path class="page-request" marker-end="url(#summary-arrow)" fill="none" stroke="currentColor" stroke-width="2" />
      <path class="page-response" marker-end="url(#summary-arrow)" fill="none" stroke="#cbd5e1" stroke-width="2" />
      <g class="page-route-labels">
        <text x="400" y="208" text-anchor="middle" fill="currentColor" style="font-size: 19px">/about</text>
        <text x="400" y="261" text-anchor="middle" fill="#cbd5e1" style="font-size: 18px">HTML</text>
      </g>
    </g>
  </g>
  <g v-click="3">
    <path d="M320 268V266Q320 258 312 258H60Q48 258 48 246V201" marker-start="url(#summary-arrow)" marker-end="url(#summary-arrow)" fill="none" stroke="#fcd34d" stroke-width="2" stroke-linecap="round" />
    <text x="10" y="290" fill="#fcd34d" font-family="monospace" style="font-size: 18px">/app.a1b2.js</text>
    <text x="10" y="316" fill="#fcd34d" font-family="monospace" style="font-size: 18px">/app.c3d4.css</text>
  </g>
</svg>

<Achievement v-click="6">Congratulations, you've caught up to Cloudflare Pages, c. 2021!</Achievement>

<style>
.summary-heading { display: flex; align-items: center; justify-content: space-between; gap: 24px; }
h1, h2 { margin: 0 !important; }
.page-roundtrip { color: #fcd34d; transition: color 750ms ease; }
.page-request {
  d: path("M470 268L470 226Q470 216 460 216L270 216Q260 216 260 206L260 201");
  transition: d 750ms cubic-bezier(0.65, 0, 0.35, 1);
}
.page-response {
  d: path("M280 201L280 230Q280 240 290 240L490 240Q500 240 500 250L500 268");
  transition: d 750ms cubic-bezier(0.65, 0, 0.35, 1);
}
.page-route-labels { transition: transform 750ms cubic-bezier(0.65, 0, 0.35, 1); }
.page-at-function { color: #67e8f9; }
.page-at-function .page-request { d: path("M470 268L470 226Q470 216 480 216L740 216Q750 216 750 206L750 201"); }
.page-at-function .page-response { d: path("M770 201L770 230Q770 240 760 240L510 240Q500 240 500 250L500 268"); }
.page-at-function .page-route-labels { transform: translateX(220px); }
@media (prefers-reduced-motion: reduce) {
  .page-roundtrip, .page-request, .page-response, .page-route-labels { transition: none; }
}

</style>

<!--
- One build, two deployment outputs.
- SSR returns HTML; JS/CSS still come from the CDN.
-->
