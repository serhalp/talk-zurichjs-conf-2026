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
<p v-click="2" class="future-aside">Remember <code>./dist/server/entry.mjs</code>?<br />We knew where it was because we knew the framework.</p>

<!--
The listing is illustrative, not the output of a particular framework. A bundler entry is a build concept. It might be a request handler, a worker, or another kind of module. Inferring the HTTP entry from the top-level bundle works only with assumptions about the framework and configuration.
This is the distinction behind https://github.com/vitejs/vite/discussions/22507
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

<p v-click="1">Fortuitously, the ecosystem has recently converged on a useful shape…</p>

<style>
.invocation-examples { display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 16px 24px; align-items: start; }
</style>

<!--
These are illustrative contracts, not attributed framework APIs. Finding the module does not tell us its export shape: named function, default function, or an object with a method. We also need inputs, outputs, and invocation: Web Request versus Node request, returning HTML or a Response versus mutating an outgoing response, and additional context.
Discovery and signature belong together. The proposed entry point API distinguishes fetchable from custom; custom is deliberately opaque to a generic consumer.
Source: https://github.com/vitejs/vite/discussions/22507
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
I made fetchable.org to document and give a name to an existing convention, not to invent a new runtime or claim to have originated this shape. Cloudflare helped popularize it; many runtimes, frameworks, and libraries use it.
The method can return Response synchronously or Promise<Response>; this example chooses async. Extra arguments and properties are allowed. Sharing the invocation shape does not make every runtime API portable.
Source: https://fetchable.org/
The logo cloud selects entries from the site's interoperability list (checked September 7, 2026). Philippe confirmed SolidStart support is complete; the site's coming-soon label is outdated. Logos downloaded from Iconify: logos (Bun, Hono, Cloudflare Workers, Solid), simple-icons (Deno, Netlify, Vercel), unjs (H3, Nitro), thesvg-color (Elysia, TanStack).
-->

---
level: 2
class: authored future-section compact-code
clicks: 2
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

<p v-click="2">Same entry name. Now the platform knows what it is.</p>

<!--
Real proposed API, abridged framework configuration. The requestEntrypoints key matches the named bundler input. It is not a second source path or a route. consumer: 'server' and other framework configuration are omitted here.
Fetchable is the default type; custom is available for contracts a generic platform cannot interpret. Multiple request entries per environment are allowed.
RFC: https://github.com/vitejs/vite/discussions/22507
Implementation PR, still open when checked September 7, 2026: https://github.com/vitejs/vite/pull/22680
This is not a released Vite API. The slide follows the RFC spelling, including rollupOptions.
-->

---
level: 2
class: authored future-section compact-code
clicks: 2
---

# <span class="gap-number">1</span><span class="gap-number">2</span> The platform can find the output.

<div class="future-status">Proposed API (platform plugin side)</div>

```ts [ZurichCloud Vite plugin]
generateBundle(_, bundle) {
  const entries =
    this.environment.getRequestEntrypointOutputs(bundle);

  for (const entry of entries) {
    const source = `
import fetchable from "./${entry.fileName}";
export default async (req) => {
  const res = await fetchable.fetch(req);
  return res;
};`;
  }
}
```

<p v-click="1" class="future-takeaway">Find the handler. Generate the ZurichCloud Function.</p>
<p v-click="2">Same job as before. No guessing which file to wrap.</p>

<!--
This is an excerpt from the proposed consumer API, not a complete deployment plugin. The loop illustrates generated function source; fetch runs at request time, not during generateBundle. Assume fetchable entries and a wrapper beside the corresponding entry chunk. Writing the source and provisioning output are omitted; a real plugin also filters applicable environments and supported entry types.
getRequestEntrypointOutputs maps the declaration to actual output chunks, avoiding assumed output filenames. Discovery alone does not supply routes or automatically dispatch requests in dev.
Source: https://github.com/vitejs/vite/discussions/22507 and https://github.com/vitejs/vite/pull/22680
-->

---
level: 2
class: authored future-section
clicks: 2
---

# <span class="gap-number">3</span> Which requests get routed where?

<RequestRouting :routed="$clicks >= 1" />

<p v-click="1" class="future-takeaway">One build can produce several request handlers ("server entry points").</p>
<p v-click="2">The framework knows the routes. The platform needs that information... sometimes.</p>

<!--
The split is illustrative: /about to SSR, /api/cart to an API handler. Not every framework or platform needs multiple bundles.
This is where React Router's user-defined serverBundles come back into the story. Our earlier Netlify plugin example cannot control those by inspecting Vite alone today. Shared entry and routing declarations could remove that framework-specific knowledge requirement; they do not solve it until frameworks publish the information.
Routing remains a design discussion: https://github.com/vitejs/vite/discussions/21212 and https://github.com/vitejs/ecosystem/issues/12
-->

---
level: 2
class: authored future-section
clicks: 4
---

# Framework adapters benefit too.

<Transition name="adapter-callback" mode="out-in">
<div v-if="$clicks < 2" key="architectures">
  <IntegrationSurfaces :focus="$clicks >= 1 ? 'framework' : 'vite'" />
</div>
<div v-else key="adapters">

<svg class="adapter-payoff" viewBox="0 0 868 244" role="img" aria-label="Astro and SvelteKit each use their ZurichCloud adapter to declare entry points and routes to the same shared ZurichCloud Vite plugin.">
  <image href="/astro.svg" x="8" y="34" width="38" height="38" class="payoff-mono" />
  <text x="62" y="60">Astro</text>
  <image href="/svelte.svg" x="8" y="162" width="38" height="38" class="payoff-mono" />
  <text x="62" y="188">SvelteKit</text>
  <g class="payoff-arrows">
    <path d="M174 54h38m-6-5 6 5-6 5" />
    <path d="M174 182h38m-6-5 6 5-6 5" />
    <path d="M452 54h34q18 0 18 18v30q0 16 18 16h30m-6-5 6 5-6 5" />
    <path d="M452 182h34q18 0 18-18v-30q0-16 18-16" />
  </g>
  <rect x="222" y="16" width="230" height="76" rx="10" />
  <text x="337" y="48" text-anchor="middle">ZurichCloud</text>
  <text x="337" y="76" text-anchor="middle">Astro adapter</text>
  <rect x="222" y="144" width="230" height="76" rx="10" />
  <text x="337" y="176" text-anchor="middle">ZurichCloud</text>
  <text x="337" y="204" text-anchor="middle">SvelteKit adapter</text>
  <text class="payoff-contract" x="337" y="125" text-anchor="middle">Entry points + routes</text>
  <rect x="562" y="70" width="298" height="96" rx="10" />
  <g transform="translate(580 98)">
    <path d="M0 0h38v38z" fill="#fff" />
    <path d="M0 0v38h38z" fill="#38bdf8" />
  </g>
  <text x="636" y="111">Shared ZurichCloud</text>
  <text x="636" y="140">Vite plugin</text>
</svg>

<p class="callback-line" :class="{ 'callback-hidden': $clicks < 3 }">The adapters know the framework. They can declare the same entry points and routes.</p>
<p class="future-takeaway callback-line" :class="{ 'callback-hidden': $clicks < 4 }">The shared plugin does the common deployment work.</p>

</div>
</Transition>

<style>
.adapter-callback-enter-active, .adapter-callback-leave-active { transition: opacity 400ms ease, transform 400ms ease; }
.adapter-callback-enter-from { opacity: 0; transform: translateY(10px); }
.adapter-callback-leave-to { opacity: 0; transform: translateY(-10px); }
.callback-line { transition: opacity 350ms ease; }
.callback-hidden { opacity: 0; }
@media (prefers-reduced-motion: reduce) { .adapter-callback-enter-active, .adapter-callback-leave-active { transition: none; } }
.adapter-payoff { width: 100%; margin: 0 0 8px; overflow: visible; }
.adapter-payoff rect { fill: #17202e; stroke: #64748b; }
.adapter-payoff text { fill: #f8fafc; font-size: 23px; }
.adapter-payoff .payoff-contract { fill: #bef264; font-size: 21px; }
.payoff-arrows { fill: none; stroke: #94a3b8; stroke-width: 1.5; stroke-linecap: round; stroke-linejoin: round; }
.payoff-mono { filter: brightness(0) invert(1); }
</style>

<!--
This is the intended architecture, not existing universal support. Astro and SvelteKit adapters can retain their framework interfaces and arrange for a platform plugin to receive common declarations. Their framework-specific features do not disappear.
Start with the exact two architecture boxes from the detour, still focused on Vite. Click 1 switches focus to the framework API side. Click 2 transitions to the adapter diagram; clicks 3 and 4 explain the delegation.
Return explicitly to the other integration path introduced before TanStack Start. For Vite-first integrations, the contracts remove missing information from the shared surface. For framework adapters, the benefit is delegating repeated deployment implementation while preserving their framework-specific API. Both reduce the same N-by-M duplication.
The Netlify Astro adapter already uses a Vite plugin for dev, which demonstrates the layering pattern. The future opportunity is sharing more production deployment logic too. Do not claim a measured percentage of deleted code.
The shared contracts could also benefit Nitro and less mainstream participating frameworks. Runtime compatibility and framework integration still matter.
Source: https://github.com/vitejs/vite/discussions/20907
-->
