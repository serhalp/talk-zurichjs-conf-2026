---
class: authored future-section
clicks: 2
---

# <span class="gap-number">1</span> Where are the request entry points?

```text [Server build output] {4}
dist/server/
├── app.mjs
├── chunks/
├── entry.mjs
└── worker.mjs
```

<p v-click="1" class="big-line">A bundle entry isn't necessarily a request entry point.</p>
<p v-click="2" class="future-aside">Remember <code>../../dist/server/entry.mjs</code>?<br />We knew where it was because we knew the framework.</p>

<!--
- Bundle entry ≠ request entry point.
-->

---
level: 2
class: authored future-section
clicks: 1
---

# <span class="gap-number">2</span> How do we invoke them?

<div class="invocation-examples">

```ts [Named export]
import { render } from "./entry.mjs";

const html = await render(url);
```

<!-- prettier-ignore -->
```ts [Default export]
import handle from "./entry.mjs";

const response =
  await handle(request, context);
```

<!-- prettier-ignore -->
```ts [A method on the default export]
import app from "./entry.mjs";

const response =
  await app.fetch(request);
```

```ts [Node request / response]
import { handle } from "./entry.mjs";

handle(nodeRequest, nodeResponse);
```

</div>

<p v-click="1">Fortuitously, the ecosystem has been converging on a convention…</p>

<style>
.invocation-examples { display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 16px 24px; align-items: start; }
</style>

<!--
- Which export? Which method? Arguments? Return value?
- Web vs Node; Response vs HTML; extra context.
-->

---
level: 2
class: authored future-section
clicks: 3
---

# <span class="gap-number">2</span> Fetchable

<div class="fetchable-anatomy">
<div v-click="2" class="fetchable-module-label">Fetchable module</div>
<svg v-click="1" class="fetchable-annotations" viewBox="0 0 210 198" aria-label="The first three lines are a fetch handler. The whole file is a fetchable module.">
  <path class="handler-bracket" d="M202 45h-12v81h12M190 85H140" />
  <text class="handler-label" x="18" y="79">Fetch handler</text>
</svg>

```ts [entry.ts]
async function fetch(request: Request): Promise<Response> {
  return new Response("Hello world");
}

export default { fetch };
```

</div>

<div v-click="3" class="fetchable-cloud">
  <div><img src="/fetchable/bun.svg" alt="" />Bun</div>
  <div><img src="/fetchable/hono.svg" alt="" />Hono</div>
  <div><img src="/fetchable/elysia.svg" alt="" />Elysia</div>
  <div><img src="/fetchable/h3.svg" alt="" />H3</div>
  <div><img src="/fetchable/nitro.svg" alt="" />Nitro</div>
  <div><img src="/fetchable/deno.svg" alt="" />Deno</div>
  <div><img src="/fetchable/cloudflare-workers.svg" alt="" />Cloudflare Workers</div>
  <div><img src="/fetchable/netlify.svg" alt="" />Netlify Functions</div>
  <div><img src="/fetchable/vercel.svg" alt="" />Vercel Functions</div>
  <div><img src="/fetchable/tanstack.svg" alt="" />TanStack Start</div>
  <div><img src="/fetchable/solid.svg" alt="" />SolidStart</div>
  <div><img src="/fetchable/deno.svg" alt="" />Deno Deploy</div>
</div>

<a v-click="3" class="future-link" href="https://fetchable.org">fetchable.org ↗</a>

<style>
.fetchable-anatomy { position: relative; padding-left: 210px; margin-top: 46px; }
.fetchable-module-label { position: absolute; left: 210px; right: 0; bottom: calc(100% + 10px); padding-bottom: 6px; border-bottom: 1.5px solid #bef264; text-align: center; color: #bef264; font-size: 19px; }
.fetchable-annotations { position: absolute; left: 0; top: 0; width: 210px; height: 198px; overflow: visible; }
.fetchable-annotations path { fill: none; stroke-width: 1.5; stroke-linecap: round; stroke-linejoin: round; }
.fetchable-annotations text { font-size: 19px; font-family: inherit; }
.handler-bracket { stroke: #c4b5fd; }
.handler-label { fill: #c4b5fd; }
.fetchable-cloud { display: flex; flex-wrap: wrap; justify-content: center; align-items: center; gap: 14px 26px; margin: 22px 12px 0; }
.fetchable-cloud > div { display: flex; align-items: center; gap: 9px; white-space: nowrap; font-size: 24px; line-height: 36px; }
.fetchable-cloud img { width: 30px; height: 30px; object-fit: contain; }
</style>

<!--
- Named an existing convention; Cloudflare helped popularize it.
- Response or Promise<Response>; extra arguments allowed.
- Common shape ≠ portable runtime APIs.
-->

---
level: 2
class: authored future-section compact-code
clicks: 1
---

# <span class="gap-number">1</span><span class="gap-number">2</span> Tell Vite which entries handle requests.

<div class="future-status">Proposed API (framework side)</div>

<CodeTokenAccent token="app" :enabled="$clicks >= 1">

<!-- prettier-ignore -->
````md magic-move [Vite config populated by framework] {at: 1} {duration:700}
```ts [Vite config populated by framework]
environments: {
  ssr: {
    build: {
      rollupOptions: {
        input: {
          app: "virtual:framework/app-entry",
          rsc: "virtual:framework/rsc-entry",
        },
      },
    },
  },
}
```
```ts [Vite config populated by framework]
environments: {
  ssr: {
    build: {
      rollupOptions: {
        input: {
          app: "virtual:framework/app-entry",
          rsc: "virtual:framework/rsc-entry",
        },
      },
    },
    requestEntrypoints: {
      app: { type: "fetchable" },
    },
  },
}
```
````

</CodeTokenAccent>

<!--
- Key matches the named build input, not a path or route.
- Fetchable by default; custom is opaque to generic plugins.
-->

---
level: 2
class: authored future-section compact-code function-generation-slide
clicks: 2
---

# <span class="gap-number">1</span><span class="gap-number">2</span> Now the platform plugin can find them

<div class="future-status">Proposed API (platform plugin side)</div>

<div class="platform-plugin-example">
<div class="code-brand-marks">
  <svg viewBox="0 0 24 24" role="img" aria-label="ZurichCloud"><path d="M1 1h22v22z" fill="#fff" /><path d="M1 1v22h22z" fill="#38bdf8" /></svg>
  <img src="/vite.svg" alt="Vite" />
</div>

<!-- prettier-ignore -->
```ts [ZurichCloud Vite plugin]
generateBundle(_, bundle) {
  const entries =
    this.environment.getRequestEntrypointOutputs(bundle);
  for (const entry of entries) { /* … */ }
}
```

</div>

<div v-click="1" class="generated-function-example">
<svg class="function-generation-arrow" viewBox="0 0 240 190" aria-label="Generate ZurichCloud Function">
  <path d="M38 -24v42q0 18 18 18h164m-7-6 7 6-7 6" />
  <text x="38" y="84">Generate</text>
  <text x="38" y="111">ZurichCloud</text>
  <text x="38" y="138">Function</text>
</svg>

<div class="generated-function-sheet">
<div class="code-brand-marks">
  <svg viewBox="0 0 24 24" role="img" aria-label="ZurichCloud"><path d="M1 1h22v22z" fill="#fff" /><path d="M1 1v22h22z" fill="#38bdf8" /></svg>
</div>
<CodeReferenceAccent active :text="$clicks >= 2 ? './app.mjs' : './${entry.fileName}'">

<!-- prettier-ignore -->
````md magic-move [.zurich/functions/ssr.mjs] {at: 2} {duration:700}
```ts [.zurich/functions/ssr.mjs]
import fetchable from "./${entry.fileName}";

export default async (req) => {
  const res = await fetchable.fetch(req);
  return res;
};
```
```ts [.zurich/functions/ssr.mjs]
import fetchable from "./app.mjs";

export default async (req) => {
  const res = await fetchable.fetch(req);
  return res;
};
```
````

</CodeReferenceAccent>
</div>
</div>

<style>
.function-generation-slide h1 { margin-bottom: 26px; }
.function-generation-slide .future-status { margin-bottom: 12px; }
.platform-plugin-example, .generated-function-sheet { position: relative; }
.platform-plugin-example :deep(pre), .platform-plugin-example :deep(code), .generated-function-sheet :deep(pre), .generated-function-sheet :deep(code) { line-height: 1.2 !important; }
.code-brand-marks { position: absolute; right: 14px; top: 7px; display: flex; align-items: center; gap: 10px; z-index: 2; pointer-events: none; }
.code-brand-marks svg, .code-brand-marks img { width: 22px; height: 22px; object-fit: contain; }
.generated-function-sheet .code-brand-marks { top: 11px; right: 14px; }
.generated-function-example { position: relative; padding-left: 240px; margin-top: 16px; transition: opacity 500ms ease; }
.function-generation-arrow { position: absolute; left: 0; top: 0; width: 240px; height: 190px; overflow: visible; }
.function-generation-arrow path { fill: none; stroke: #94a3b8; stroke-width: 1.5; stroke-linecap: round; stroke-linejoin: round; }
.function-generation-arrow text { fill: #67e8f9; font-size: 23px; }
.generated-function-sheet { border: 1px dashed #67e8f9; border-radius: 8px; padding: 6px; background: #67e8f905; }
</style>

<!--
- Generate at build time; invoke at request time.
- Actual output filename, no guessing. Routing still missing.
-->

---
level: 2
class: authored future-section
clicks: 3
---

# <span class="gap-number">3</span> Which requests get routed where?

<RequestRouting :routed="$clicks >= 1" />

<p class="future-takeaway">One build can produce &gt;1 request handlers ("server entry points").</p>
<p v-click="2" class="future-takeaway">The framework knows how to route, but doesn't tell Vite.</p>
<p v-click="3" class="future-takeaway">So the platform can't know.</p>

<!--
- Only matters when splitting handlers.
- RR serverBundles: callback to the earlier limitation.
- Need routing as build-time configuration, not just a router function.
-->

---
level: 2
class: authored future-section
clicks: 5
---

# Framework adapters benefit too.

<div class="adapter-callback-stack">
<div class="adapter-callback-phase" :class="{ 'callback-hidden': $clicks >= 2 }">
  <IntegrationSurfaces :focus="$clicks >= 1 ? 'framework' : 'vite'" />
</div>
<div class="adapter-callback-phase" :class="{ 'callback-hidden': $clicks < 2 }">

<p class="adapter-sketch-label"><img src="/zurich-cloud-symbol.svg" alt="" /><img src="/svelte.svg" alt="" class="adapter-framework-logo" />ZurichCloud SvelteKit adapter</p>

<AdapterMinimap :highlight="$clicks >= 3" :delegated="$clicks >= 4" :astro="$clicks >= 5" />

</div>
</div>

<style>
.adapter-callback-stack { display: grid; }
.adapter-callback-phase { grid-area: 1 / 1; min-width: 0; transition: opacity 450ms ease, transform 450ms ease; }
.adapter-sketch-label { display: flex; align-items: center; gap: 10px; margin: 0 0 8px; padding-left: 2.304%; color: #f8fafc; font-size: 24px; }
.adapter-sketch-label img { width: 28px; height: 28px; }
.adapter-framework-logo { filter: brightness(0) invert(1); }
.callback-line { margin-top: 24px; transition: opacity 350ms ease; }
.callback-hidden { opacity: 0; pointer-events: none; visibility: hidden; }
.adapter-callback-phase.callback-hidden { transform: translateY(10px); }
@media (prefers-reduced-motion: reduce) { .adapter-callback-phase, .callback-line { transition: none; } }
</style>

<!--
- ~70% is my estimate, not a measured deletion.
- Keep framework semantics; delegate packaging + serialization.
- Work moves into one plugin, doesn’t disappear.
-->
