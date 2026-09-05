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

<svg v-click="2" viewBox="0 0 868 174" class="ssr-flow" role="img" aria-label="A cat represents the visitor using a browser to request hello.zurich.cloud/about. A ZurichCloud server calls Nuxt and returns the rendered About page.">
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
  <image href="/zurichjs.svg" x="609" y="20" width="142" height="22"><title>ZurichCloud</title></image>
  <text x="851" y="37" text-anchor="end" fill="#cbd5e1" style="font-size: 18px">Server</text>
  <rect x="614" y="60" width="232" height="90" rx="8" fill="#132a32" stroke="#67e8f9" stroke-width="2" />
  <image href="/nuxt.svg" x="634" y="73" width="34" height="28" style="filter: brightness(0) invert(1)" />
  <text x="682" y="96" fill="#e2e8f0" style="font-size: 24px">Nuxt</text>
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
The user wants to render pages at request time. Introduce frameworks that support this before diving into our toy framework or the platform mechanics.

Click 1: server-side rendering, or SSR. Show the framework logos together, with the same automatic stagger as the SSG and bundler rows. These frameworks also support other rendering modes; this slide only introduces their ability to render pages in response to requests.

Click 2: reuse the browser, cat, and /about URL. The request reaches a ZurichCloud server, which calls Nuxt to render the page and returns HTML to the browser. The render(request) label is conceptual pseudocode, not a literal public Nuxt API. Keep this about pages; API handlers and server functions come later.

No account-page or authentication example here. The next slides explain the browser/server split, deployment shapes, and how the platform invokes the framework.
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
  <image href="/zurichjs.svg" x="642" y="18" width="148" height="24" />
  <rect x="642" y="59" width="204" height="58" rx="8" fill="#132a32" stroke="#67e8f9" />
  <text x="744" y="95" text-anchor="middle" fill="#67e8f9" font-family="monospace" style="font-size: 24px">hello.ts</text>
</svg>

<style>
h1 { margin-bottom: 12px !important; }
</style>

<!--
[Section 2: about 5 minutes total.]

We've glossed over the infrastructure so far. To render pages on demand, ZurichCloud needs a new way to run the user's code. Let's introduce serverless functions.

This is our made-up convention: put a TypeScript module in .zurich/. ZurichCloud prepares it to run on the server and calls its default export with a web Request. It returns a web Response. These modules aren't public files.

Click 1: request /functions/hello and ZurichCloud invokes hello.ts. The visitor is outside the browser, as on slide 9.

Click 2: the returned response appears in the browser. We take care of running the code when a request comes in; the user doesn't start a server process.

The exported config maps /functions/hello to this function. The directory and configuration are fictional ZurichCloud conventions, not Netlify APIs. This is the missing platform capability, before we talk about integrating frameworks.
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
What if we generate that function when we build the user's site?

Same kind of function. Instead of returning Hello world, it asks the framework to render a page and returns the HTML.

Initially: import the framework's server entry point. The import and render signature are illustrative, not an actual Nuxt API.

Click 1: add the function, with placeholder HTML and a text/html response.

Click 2: replace the placeholder with await render(request). We generate the wrapper at build time; the renderer runs later, when a request arrives.

Click 3: add the routing config.

The generated config routes requests matching /* to this function. We will return to routing and the relationship with static assets later.

Now we can return to the question of where the renderer comes from, and how to call it. Static assets still use the file-serving path we've already built.
-->

---
level: 2
class: authored
---

<div class="summary-heading">

# The story so far

<LevelBadge :number="5">Full stack</LevelBadge>

</div>

<svg class="mt-5" viewBox="0 0 868 350" role="img" aria-label="One build deploys static assets to the CDN and server code to ZurichCloud Functions. The visitor requests a rendered page from a function, then JavaScript and CSS from the CDN.">
  <rect x="284" y="1" width="300" height="62" rx="10" fill="#132a32" stroke="#67e8f9" stroke-width="2" />
  <text x="434" y="23" text-anchor="middle" fill="#cbd5e1" font-family="monospace" style="font-size: 18px">build_command</text>
  <text x="434" y="49" text-anchor="middle" fill="#67e8f9" font-family="monospace" style="font-size: 22px">$ nuxt build</text>
  <g v-click="1">
    <path d="M334 63V83H175V133l-6 -9m6 9l6 -9 M534 63V83H693V133l-6 -9m6 9l6 -9" fill="none" stroke="#94a3b8" stroke-width="2" />
    <rect x="30" y="88" width="290" height="29" fill="#111111" />
    <text x="175" y="109" text-anchor="middle" fill="#fcd34d" font-family="monospace" style="font-size: 18px">publish_dir: dist/client/</text>
    <rect x="594" y="88" width="198" height="29" fill="#111111" />
    <text x="693" y="109" text-anchor="middle" fill="#67e8f9" font-family="monospace" style="font-size: 18px">.zurich/ssr.ts</text>
    <rect x="10" y="135" width="330" height="86" rx="12" fill="#1b2416" stroke="#bef264" stroke-width="2" />
    <image href="/zurichjs.svg" x="28" y="150" width="142" height="23" />
    <text x="320" y="171" text-anchor="end" fill="#f8fafc" style="font-size: 24px">CDN</text>
    <text x="175" y="202" text-anchor="middle" fill="#fcd34d" style="font-size: 22px">Static files</text>
    <rect x="528" y="135" width="330" height="86" rx="12" fill="#1b2416" stroke="#bef264" stroke-width="2" />
    <image href="/zurichjs.svg" x="546" y="150" width="142" height="23" />
    <text x="840" y="171" text-anchor="end" fill="#f8fafc" style="font-size: 24px">Functions</text>
    <text x="693" y="202" text-anchor="middle" fill="#67e8f9" font-family="monospace" style="font-size: 22px">render(request)</text>
  </g>
  <g v-click="2">
    <image href="/patak-cat.png" x="212" y="281" width="62" height="62" />
    <rect x="294" y="276" width="400" height="71" rx="10" fill="#17202e" stroke="#64748b" stroke-width="2" />
    <path d="M294 309H694" stroke="#64748b" />
    <text x="310" y="299" fill="#e2e8f0" font-family="monospace" style="font-size: 18px">hello.zurich.cloud/<tspan fill="#f0abfc">about</tspan></text>
    <text x="310" y="335" fill="#f8fafc" style="font-size: 22px">About Zurich</text>
    <path d="M710 310H814V233l-6 9m6 -9l6 9" fill="none" stroke="#67e8f9" stroke-width="2" />
    <text x="792" y="253" text-anchor="end" fill="#67e8f9" style="font-size: 19px">/about</text>
    <text x="792" y="279" text-anchor="end" fill="#cbd5e1" style="font-size: 19px">← HTML</text>
  </g>
  <g v-click="3">
    <path d="M320 276V263H44V233l-6 9m6 -9l6 9" fill="none" stroke="#fcd34d" stroke-width="2" />
    <text x="10" y="290" fill="#fcd34d" font-family="monospace" style="font-size: 18px">/app.a1b2.js</text>
    <text x="10" y="316" fill="#fcd34d" font-family="monospace" style="font-size: 18px">/app.c3d4.css</text>
  </g>
</svg>

<Achievement v-click="4">Congratulations, you've caught up to Cloudflare Pages, c. 2021!</Achievement>

<style>
.summary-heading { display: flex; align-items: center; justify-content: space-between; gap: 24px; }
h1, h2 { margin: 0 !important; }
</style>

<!--
The story so far: one build can prepare both parts of the deployment. Use nuxt build as the concrete build command. The output paths and ZurichCloud integration remain illustrative, not Nuxt defaults.

Click 1: publish_dir selects the static files for the CDN. Separately, the generated ZurichCloud function calls the built server entry. Server code is not uploaded as public files. The diagram abbreviates the server output to its generated function wrapper.

Click 2: the visitor asks for /about. ZurichCloud invokes the SSR function and sends the HTML back to the browser.

Click 3: that HTML references JavaScript and CSS. The browser requests those files from the same site, and the CDN serves them. The filenames are illustrative content hashes. The browser runs the JavaScript; the CDN serves bytes.

Click 4: Cloudflare Pages added integrated functions in beta on November 17, 2021. This milestone is about deploying static files and functions together, not the exact runtime or API shown here. Source: https://blog.cloudflare.com/cloudflare-pages-goes-full-stack/

We are glossing over infrastructure topology. CDN files and functions are distinct deployment outputs, not necessarily distinct public hostnames. In this fictional platform, existing static files take precedence over the /* SSR fallback. We will return to routing later.
-->
