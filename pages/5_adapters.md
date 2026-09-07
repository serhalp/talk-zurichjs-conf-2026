---
class: authored
---

# Wait. What happened to zero config?

<LevelDown :lost="$clicks >= 1" />

<div class="wrapper-questions" :class="{ 'frameworks-expanded': $clicks >= 6 }">
<div class="wrapper-code">

<!-- prettier-ignore -->
```ts [.zurich/ssr.ts]
import { render } from
  "./dist/server/entry.mjs";

export default async (request: Request) => {
  const html = await render(request);
  return new Response(html, {
    headers: { "Content-Type": "text/html" },
  });
};
```

</div>
<div class="question-panel">
  <Transition name="question-swap">
    <div v-if="$clicks < 5" key="questions" class="questions">
      <p v-click="2">How will users know they need this?</p>
      <p v-click="3">Should they copy this from our docs?</p>
      <p v-click="4">Should this be in a bespoke template?</p>
    </div>
    <div v-else key="logos" class="framework-list">
      <ToolLogos :revealed="$clicks >= 5" :logos="[
        { name: 'Astro', src: '/astro.svg' },
        { name: 'SvelteKit', src: '/svelte.svg' },
        { name: 'React Router', src: '/reactrouter.svg' },
        { name: 'Nuxt', src: '/nuxt.svg' },
        { name: 'Next.js', src: '/nextjs.svg' },
      ]" />
      <ToolLogos v-if="$clicks >= 8" :revealed="true" :logos="[
        { name: 'TanStack Start', src: '/tanstack.svg' },
        { name: 'SolidStart', src: '/solid.svg' },
        { name: 'Qwik', src: '/qwik.svg' },
        { name: 'Analog', src: '/analog.svg' },
        { name: 'Angular', src: '/angular.svg' },
      ]" />
      <div v-if="$clicks >= 9" class="long-tail">
        <ToolLogos :revealed="true" :logos="[
          { name: 'Fresh', src: '/fresh.svg', color: true },
          { name: 'Waku', src: '/waku.svg', color: true },
          { name: 'Cedar', src: '/cedar.png', color: true },
          { name: 'Hydrogen', src: '/hydrogen.svg' },
        ]" />
        <span class="more-frameworks" aria-label="And more">…</span>
      </div>
    </div>
  </Transition>
</div>
</div>

<div class="framework-costs">
  <p v-click="7" class="framework-differences">This code will be different for each framework…<span v-click="10" class="text-[#67e8f9]"><br>…and each framework version.</span></p>
  <div v-click="11" class="maintenance-costs">
    <p>High maintenance burden for ZurichCloud</p>
    <p v-click="12">Poor DX for users</p>
  </div>
</div>

<style>
h1 { margin-bottom: 18px !important; }
.wrapper-questions { position: relative; display: grid; grid-template-columns: minmax(0, 1.5fr) minmax(0, 1fr); gap: 28px; }
.wrapper-code { transition: opacity 350ms ease; }
.frameworks-expanded .wrapper-code { opacity: 0; pointer-events: none; height: 264px; overflow: hidden; }
.question-panel { position: absolute; top: 0; bottom: 0; right: 0; width: calc(40% - 11.2px); transition: width 650ms cubic-bezier(0.65, 0, 0.35, 1); }
.frameworks-expanded .question-panel { width: 100%; }
.frameworks-expanded .framework-list { display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 28px; }
.frameworks-expanded .framework-list :deep(.tool-logos) { padding-left: 0; gap: 12px; }
.long-tail :deep(.tool-logos) { justify-content: flex-start; }
.more-frameworks { display: block; margin: 12px 0 0 52px; color: #94a3b8; font-size: 40px; line-height: 40px; animation: framework-arrival 450ms ease 900ms both; }
.questions, .framework-list { position: absolute; inset: 0; }
.questions { display: flex; flex-direction: column; justify-content: center; gap: 16px; }
.questions p { margin: 0; font-size: 24px; line-height: 1.25; }
.framework-list :deep(.tool-logos) { flex-direction: column; margin-top: 12px; gap: 18px; }
.framework-list :deep(.tool-logo) {
  animation: framework-arrival 450ms cubic-bezier(0.16, 1, 0.3, 1) both;
  animation-delay: calc(150ms + var(--logo-index) * 220ms);
}
@keyframes framework-arrival {
  from { opacity: 0; transform: translateX(20px) scale(0.96); }
  to { opacity: 1; transform: translateX(0) scale(1); }
}
.framework-costs { display: grid; grid-template-columns: 1.5fr 1fr; gap: 28px; margin-top: 28px; line-height: 1.25; }
.framework-differences { margin: 0; white-space: nowrap; }
.maintenance-costs { border-left: 2px solid #64748b; padding-left: 18px; }
.maintenance-costs p { margin: 0; }
.maintenance-costs p + p { margin-top: 10px; }
.question-swap-enter-active, .question-swap-leave-active { transition: opacity 350ms ease, transform 350ms ease; }
.question-swap-enter-from { opacity: 0; transform: translateY(12px); }
.question-swap-leave-to { opacity: 0; transform: translateY(-12px); }
@media (prefers-reduced-motion: reduce) {
  .question-swap-enter-active, .question-swap-leave-active { transition: none; }
  .framework-list :deep(.tool-logo), .more-frameworks { animation: none; }
  .wrapper-code, .question-panel { transition: none; }
}
</style>

<!--
[Section 5 draft: aim for about 5 minutes across these nine slides.]

Wait. We already unlocked zero config at level 4. Now we've reached full stack, and we're asking the user to write this little function? Start with Level 5 and two ability tabs: Full stack and Zero config.

These two lines know where the framework's server entry point is and how to call it. The import and render API are still illustrative. This repeats the previous slide's convention to make the connection immediate; it is not a real Astro entry point.

Click 1: cross out Zero config and play two automatic level-down beats: 5 to 4, then 4 to 3. This is the joke that manual deployment glue has taken us back to the build-only experience. Full stack remains visible as the capability we are trying to automate.

Click 2: how will users know they need this?

Click 3: should they copy it from our docs?

Click 4: should this be in a bespoke template?

Click 5: the questions transition to Astro, SvelteKit, React Router, Nuxt, and Next.js, appearing one by one without additional clicks.

Click 6: fade out the code and move the first five logos to the left. Reserve three columns so later groups appear without shifting the existing logos.

Click 7: this code will be different for each framework.

Click 8: add TanStack Start, SolidStart, Qwik, Analog, and Angular one by one in the second column.

Click 9: add Fresh, Waku, Cedar, and Hydrogen in the third column, followed by an ellipsis. The list keeps going.

Click 10: and each framework version. We need to maintain compatibility over time; this doesn't mean every release changes the wrapper.

Click 11: high maintenance burden for ZurichCloud.

Click 12: poor DX for users.

Additional logo sources: https://waku.gg/, https://cedarjs.com/, https://hydrogen.shopify.dev/.

The full config and routing aren't repeated in this excerpt. Don't imply that every framework release breaks its public APIs.
-->

---
level: 2
class: authored
---

# Let's generate it instead

<div v-click="5" class="absolute right-14 top-8">
  <LevelRecovery :active="$clicks >= 5" />
</div>

<p class="mb-7">The user installs an integration. It runs during the build.</p>

<svg viewBox="0 0 868 218" role="img" aria-label="The ZurichCloud Astro Adapter takes Astro build information and generates static assets, ZurichCloud Functions, and other deployment output for ZurichCloud.">
  <rect x="2" y="62" width="160" height="80" rx="12" fill="#17202e" stroke="#64748b" stroke-width="2" />
  <image href="/astro.svg" x="26" y="86" width="28" height="30" style="filter: brightness(0) invert(1)" />
  <text x="68" y="111" fill="#f8fafc" style="font-size: 26px">Astro</text>
  <path d="M178 102H242l-9 -6m9 6l-9 6" fill="none" stroke="#94a3b8" stroke-width="2" />
  <rect x="258" y="32" width="208" height="140" rx="12" fill="#17202e" stroke="#64748b" stroke-width="2" />
  <image href="/zurich-cloud.svg" x="280" y="48" width="120" height="26" />
  <image href="/astro.svg" x="416" y="46" width="28" height="30" style="filter: brightness(0) invert(1)" />
  <text x="362" y="111" text-anchor="middle" fill="#f8fafc" style="font-size: 24px">ZurichCloud</text>
  <text x="362" y="143" text-anchor="middle" fill="#f8fafc" style="font-size: 24px">Astro Adapter</text>
  <g v-click="1">
    <path d="M482 102H546l-9 -6m9 6l-9 6" fill="none" stroke="#94a3b8" stroke-width="2" />
    <rect x="562" y="2" width="304" height="212" rx="12" fill="#1b2416" stroke="#bef264" stroke-width="2" />
    <image href="/zurich-cloud.svg" x="582" y="20" width="176" height="27" />
    <text x="582" y="78" fill="#fcd34d" style="font-size: 24px">Static files</text>
    <text x="582" y="108" fill="#67e8f9" style="font-size: 24px">ZurichCloud Functions</text>
    <text x="582" y="138" fill="#e2e8f0" style="font-size: 24px">Redirects</text>
    <text x="582" y="168" fill="#e2e8f0" style="font-size: 24px">Headers</text>
    <text x="582" y="198" fill="#e2e8f0" style="font-size: 24px">…</text>
  </g>
</svg>

<div class="adapter-benefits">
  <p v-click="2">We can ship a fix in a patch.</p>
  <p v-click="3">... add support for a new Astro feature in a minor.</p>
  <p v-click="4">... depend on typed, documented Astro interfaces.</p>
  <p v-click="6" class="text-[#bef264]">Let's build the ZurichCloud Astro adapter.</p>
</div>

<style>
.adapter-benefits { margin-top: 0; }
.adapter-benefits p { margin: 0; line-height: 1.25; }
.adapter-benefits p + p { margin-top: 6px; }
.adapter-benefits p:last-child { margin-top: 14px; }
</style>

<!--
An adapter packages the platform-specific work we've been doing by hand. It participates in the build, knows how to call the framework, and prepares output for the deployment platform.

Click 1: that includes copying static files, preparing function entry points and their dependencies, and translating routing and other configuration. Not every framework or adapter needs all of these steps.

Click 2: a fix can now be distributed in a patch. Users still have to receive that update and rebuild; dependencies don't update themselves. We stop asking users to hand-edit the generated wrapper.

Click 3: add support for a new Astro feature in a minor.

Click 4: depend on typed, documented Astro interfaces.

Click 5: reveal the level badge in the top right and automatically level up from 3 to 4 to 5.

Click 6: let's build the ZurichCloud Astro adapter.

Keep this about the integration. No need to introduce another toy framework or repeat all of the SSR code we just built.
-->

---
level: 2
class: authored
clicks: 18
---

# ZurichCloud Astro adapter

<img src="/astro.svg" alt="" class="absolute right-14 top-10 w-12 h-12 brightness-0 invert" />

<div v-if="$clicks < 1">

<p class="mb-6">The user installs our adapter:</p>

```ts [astro.config.ts] {2,6}
import { defineConfig } from "astro/config";
import zurichCloud from "@astrojs/zurich-cloud";

export default defineConfig({
  output: "server",
  adapter: zurichCloud(),
});
```

</div>
<div v-else-if="$clicks === 1">

<!-- prettier-ignore -->
```ts [AstroIntegration API overview]
import type { AstroIntegration } from "astro";

const integration: AstroIntegration = {
  name: "…",
  hooks: {
    "astro:config:setup": ({ updateConfig }) => { /* … */ },
    "astro:config:done": ({ config, setAdapter }) => { /* … */ },
    "astro:build:setup": ({ vite, pages }) => { /* … */ },
    "astro:build:ssr": ({ manifest, middlewareEntryPoint }) => { /* … */ },
    "astro:build:done": ({ dir, pages, assets }) => { /* … */ },
    // …
  },
};
```

</div>
<EntrypointTransition v-else :active="$clicks >= 15" path="@astrojs/zurich-cloud/server" style="--slidev-code-line-height: 1.25">

````md magic-move [@astrojs/zurich-cloud/index.ts] {at:3} {duration:700}
```ts
import type { AstroIntegration } from "astro";

export default function zurichCloud(): AstroIntegration {
  return {
    name: "@astrojs/zurich-cloud",
    hooks: {},
  };
}
```

```ts
import type { AstroIntegration } from "astro";

export default function zurichCloud(): AstroIntegration {
  return {
    name: "@astrojs/zurich-cloud",
    hooks: {
      "astro:config:done": ({ setAdapter }) => {
        setAdapter({
          name: "@astrojs/zurich-cloud",
          entrypointResolution: "auto",
          serverEntrypoint: "@astrojs/zurich-cloud/server",
        });
      },
    },
  };
}
```

```ts {all|7-14}
import type { AstroIntegration } from "astro";

export default function zurichCloud(): AstroIntegration {
  return {
    name: "@astrojs/zurich-cloud",
    hooks: {
      "astro:config:done": ({ setAdapter }) => {
        setAdapter({
          name: "@astrojs/zurich-cloud",
          entrypointResolution: "auto",
          serverEntrypoint: "@astrojs/zurich-cloud/server",
          supportedAstroFeatures: { serverOutput: "stable" },
        });
      },
    },
  };
}
```

```ts
"astro:config:done": ({ setAdapter }) => {
  setAdapter({
    name: "@astrojs/zurich-cloud",
    entrypointResolution: "auto",
    serverEntrypoint: "@astrojs/zurich-cloud/server",
    supportedAstroFeatures: { serverOutput: "stable" },
  });
},
```

```ts {9-13}
"astro:config:done": ({ setAdapter }) => {
  setAdapter({
    name: "@astrojs/zurich-cloud",
    entrypointResolution: "auto",
    serverEntrypoint: "@astrojs/zurich-cloud/server",
    supportedAstroFeatures: { serverOutput: "stable" },
  });
},
"astro:config:setup": ({ config, updateConfig }) => {
  updateConfig({
    /* … */
  });
},
```

```ts {9-18|12|13|14|16|5,13-14|5}
"astro:config:done": ({ setAdapter }) => {
  setAdapter({
    name: "@astrojs/zurich-cloud",
    entrypointResolution: "auto",
    serverEntrypoint: "@astrojs/zurich-cloud/server",
    supportedAstroFeatures: { serverOutput: "stable" },
  });
},
"astro:config:setup": ({ config, updateConfig }) => {
  updateConfig({
    build: {
      client: new URL("./dist/client/", config.root),
      server: new URL("./.zurich/", config.root),
      serverEntry: "ssr.mjs",
    },
    vite: { ssr: { noExternal: true } },
  });
},
```
````

<template #runtime>
<div class="astro-runtime">

````md magic-move [@astrojs/zurich-cloud/server] {at:16} {duration:700}
```ts
export default async (request: Request) => {
  return new Response("…");
};

export const config = {
  path: "/*",
};
```

```ts
import { createApp } from "astro/app/entrypoint";

const app = createApp();

export default async (request: Request) => {
  return new Response("…");
};

export const config = {
  path: "/*",
};
```

```ts
import { createApp } from "astro/app/entrypoint";

const app = createApp();

export default async (request: Request) => {
  const response = await app.render(request);
  return response;
};

export const config = {
  path: "/*",
};
```

```ts
import { createApp } from "astro/app/entrypoint";

const app = createApp();

export default async (request: Request) => {
  const response = await app.render(request);
  for (const cookie of app.setCookieHeaders(response)) {
    response.headers.append("Set-Cookie", cookie);
  }
  return response;
};

export const config = {
  path: "/*",
};
```
````

</div>
</template>
</EntrypointTransition>

<style>
h1 { margin-bottom: 16px !important; }
.astro-runtime :deep(pre), .astro-runtime :deep(code) { line-height: 1.25 !important; }
</style>

<!--
Start with the end user's configuration. The package name @astrojs/zurich-cloud is fictional; the configuration follows Astro's documented adapter API. The server output setting makes pages render on demand by default.

Highlight the adapter import and configuration from the start. The user selects the deployment adapter here; the adapter handles the platform-specific work.

Click 1: replace the user configuration with an overview of the integration API used by adapters. These are documented hook names and arguments, with bodies omitted. Configuration hooks can change settings and register the adapter; build hooks expose Vite configuration, page information, the SSR manifest, middleware entry point, and final output. The final ellipsis indicates more hooks exist.

Click 2: start our implementation with the typed factory, package name, and an empty hooks object.

Click 3: animate in astro:config:done and the setAdapter call, registering the adapter's name and server entry point.

Click 4: add the declaration of support for server output.

Click 5: fade everything except the body of hooks, including the complete astro:config:done hook.

Click 6: animate the hooks body up to the top, removing the surrounding integration boilerplate.

Click 7: fade the existing hook and animate in astro:config:setup with only a placeholder updateConfig call.

astro:config:setup runs while Astro is setting up the user's configuration, before it is finalized. updateConfig merges our adapter's settings into it, including build output paths and Vite options. astro:config:done runs after configuration is resolved.

Click 8: fill in updateConfig while keeping the previous hook faded. This is the body of hooks; setup runs before done regardless of property order. Astro's documented build.server and build.serverEntry settings place the built runtime at .zurich/ssr.mjs; build.client keeps public output separate. Vite ssr.noExternal bundles JavaScript dependencies rather than leaving package imports for the deployment to resolve. This is a simple Node-target example; native modules and file-system assets need additional packaging in a production adapter.

Click 9: client selects where Astro writes public files for the CDN.

Click 10: server selects where Astro writes the server build.

Click 11: serverEntry names the generated function entry file, ssr.mjs.

Click 12: vite.ssr.noExternal bundles server JavaScript dependencies rather than leaving external package imports.

Click 13: highlight serverEntrypoint, build.server, and build.serverEntry together. serverEntrypoint is the adapter's input module; serverEntry names the output file Astro builds it into. build.server places that file under .zurich/.

Click 14: highlight only serverEntrypoint, fading the rest of the hooks.

Click 15: move that exact module path from the code into the runtime's filename label, then reveal its implementation. The label deliberately matches the import specifier; the source file in the package is server.ts. With entrypointResolution auto, Astro builds this module with the application's manifest and server code. createApp and render are real Astro APIs. render returns a Response, unlike the illustrative HTML renderer earlier. Forward Astro's cookie headers as the real Netlify adapter does. The default handler and path config are the ZurichCloud function contract established earlier.

The runtime initially shows only a basic ZurichCloud Function returning a placeholder Response, with its catch-all path config.

Click 16: add the createApp import and initialize Astro's application outside the handler.

astro/app/entrypoint is Astro's public runtime API for adapter authors. Its createApp() returns the Astro application instance that our handler calls with app.render(request) to get a standard Response. This is provided by Astro; @astrojs/zurich-cloud/server is our platform-specific wrapper around it. createApp was added in Astro 6.

Reference: https://docs.astro.build/en/reference/modules/astro-app/#createapp

Click 17: replace the placeholder response with app.render(request).

Click 18: forward Astro's Set-Cookie headers onto the response.

This is a minimal SSR path using real Astro APIs with a fictional deployment target and package name, not full production support for every Astro feature. The package exports its integration and server modules; the server source is TypeScript and its built package export resolves the server specifier. The broader redirects, image services, sessions, dev integration, and platform packaging are outside this excerpt.

Sources: https://docs.astro.build/en/guides/integrations-guide/netlify/ ; https://docs.astro.build/en/reference/adapter-reference/ ; https://docs.astro.build/en/reference/integrations-reference/

Implementation references: https://github.com/withastro/astro/blob/main/packages/integrations/netlify/src/index.ts ; https://github.com/withastro/astro/blob/main/packages/integrations/netlify/src/ssr-function.ts ; https://docs.astro.build/en/reference/configuration-reference/#buildserverentry ; https://vite.dev/config/ssr-options#ssr-noexternal
-->

---
level: 2
class: authored
clicks: 4
---

# One more thing...

<img src="/astro.svg" alt="" class="absolute right-14 top-10 w-12 h-12 brightness-0 invert" />

<div class="astro-rules">
<div>

<p class="rules-label">The user can tell Astro:</p>

```ts [astro.config.ts]
redirects: {
  "/old": "/new",
},
```

<div v-click="2" class="mt-5">

<!-- prettier-ignore -->
```astro [src/pages/about.astro]
---
export const prerender = true;
Astro.response.headers.set(
  "Cache-Control",
  "public, max-age=3600",
);
---
<h1>About Zurich</h1>
```

</div>
</div>
<div v-click="1" class="generated-rules">

<p class="rules-label">Our adapter tells ZurichCloud:</p>

<!-- prettier-ignore -->
````md magic-move [zurich.json (generated rules)] {at:3} {duration:700}
```json
{
  "redirects": {
    "/old": {
      "to": "/new", "status": 301
    }
  }
}
```

```json
{
  "redirects": {
    "/old": {
      "to": "/new", "status": 301
    }
  },
  "headers": {
    "/about": {
      "Cache-Control": "public, max-age=3600"
    }
  }
}
```
````

<p v-click="4" class="copy-paste-payoff">More and more code we're glad users don't have to copy-paste!</p>

</div>
</div>

<style>
h1 { margin-bottom: 20px !important; }
.astro-rules { display: grid; grid-template-columns: 1fr 1fr; gap: 36px; --slidev-code-line-height: 1.25; }
.rules-label { margin: 0 0 12px; }
.astro-rules :deep(pre), .astro-rules :deep(code) { line-height: 1.25 !important; }
.generated-rules :deep(pre), .generated-rules :deep(code) { line-height: 1.15 !important; }
.copy-paste-payoff { margin: 12px 0 0; line-height: 1.2; }
</style>

<!--
Remember how we didn't want users to copy-paste the deployment glue? They already told Astro what redirects and headers they want. They shouldn't have to repeat that in zurich.json. Our adapter translates it for them. Aim for 30–45 seconds; no second implementation deep dive.

Initially: Astro's redirects configuration. A string destination defaults to a permanent 301 redirect for GET requests.

Click 1: the adapter translates it to the ZurichCloud format introduced earlier. It can read config.redirects from astro:config:done; real adapters also inspect resolved routes to handle route patterns and generated destinations. This example deliberately uses only fixed paths.

Click 2: a prerendered Astro page sets a response header during the build. The page is static; the CDN needs the header rule because no function will run when this file is requested.

Click 3: add the corresponding ZurichCloud header rule. To implement this, the adapter opts into adapterFeatures.staticHeaders in setAdapter. Astro then exposes routeToHeaders to astro:build:generated, which the adapter serializes into the platform's header rules. This is documented since Astro 6; the earlier SSR-only excerpt did not enable or implement this extra capability.

Click 4: more and more code we're glad users don't have to copy-paste.

The JSON is the generated portion of ZurichCloud deployment configuration, merged with the user's settings; do not overwrite the user's zurich.json. The filename recalls our existing platform format. /about assumes the clean-URL mapping already established in the talk; real adapters must account for trailing-slash and output-format settings. Existing files and explicit redirect rules take precedence over the catch-all function.

The adapter writes platform-specific configuration from framework information. Dynamic responses still set their own headers at runtime. Cookie handling in the previous example is unchanged.

Sources: https://docs.astro.build/en/reference/configuration-reference/#redirects ; https://docs.astro.build/en/reference/adapter-reference/#staticheaders ; https://github.com/withastro/astro/blob/main/packages/integrations/netlify/src/index.ts
-->

---
level: 2
class: authored
---

# ZurichCloud Astro adapter

<div class="absolute right-14 top-8 z-50 flex items-center gap-4">
  <LevelBadge :number="5" class="!mb-0">Full stack</LevelBadge>
  <AstroLanding />
</div>

```sh
$ astro build
```

<div class="astro-build-output">

```text [Build output]
dist/client/         # Publish directory
  _astro/            # Browser JS + CSS
  …
.zurich/
  ssr.mjs            # Our handler + Astro's server code
  …                  # Supporting server chunks and assets
```

</div>

<p class="mt-6">ZurichCloud serves the <span class="text-[#fcd34d]">static files</span> and runs the <span class="text-[#67e8f9]">ZurichCloud Function</span>.</p>

<style>
h1 { margin-bottom: 16px !important; }
.astro-build-output :deep(.line:nth-child(-n+3) span) { color: #fcd34d !important; }
.astro-build-output :deep(.line:nth-child(n+4) span) { color: #67e8f9 !important; }
</style>

<!--
After the runtime and redirects/headers examples, connect the build to its output. Astro emits .zurich/ssr.mjs directly. ZurichCloud packages that entry together with its supporting chunks/assets, reads its config export, and publishes dist/client separately. The adapter also generates the deployment rules from the preceding slide. Static files and explicit redirect rules take precedence over the catch-all function.
-->

---
level: 2
class: authored
clicks: 12
---

# ZurichCloud SvelteKit adapter

<img src="/svelte.svg" alt="" class="absolute right-14 top-10 w-12 h-12 brightness-0 invert" />

<div v-if="$clicks === 0">

<p class="mb-6">The user installs our adapter:</p>

```ts [svelte.config.js] {1,5}
import zurichCloud from "@sveltejs/adapter-zurich-cloud";

export default {
  kit: {
    adapter: zurichCloud(),
  },
};
```

</div>
<div v-else-if="$clicks === 1" class="svelte-code">

```ts [Adapter and Builder API]
interface Adapter {
  name: string;
  adapt(builder: Builder): void | Promise<void>;
  // …
}

interface Builder {
  writeClient(dest: string): string[];
  writePrerendered(dest: string): string[];
  writeServer(dest: string): string[];
  generateManifest(opts: { relativePath: string }): string;
  generateFallback(dest: string): Promise<void>;
  getBuildDirectory(name: string): string;
  // …
}
```

</div>
<div v-else style="--slidev-code-line-height: 1.25">

<CodeReferenceAccent :active="$clicks >= 10" text="./entrypoint.ts">

<div class="svelte-adapter-file">

<!-- prettier-ignore -->
````md magic-move [@sveltejs/adapter-zurich-cloud/index.ts] {at:3} {duration:700}
```ts
import type { Adapter } from "@sveltejs/kit";

export default function zurichCloud(): Adapter {
  return {
    name: "@sveltejs/adapter-zurich-cloud",
    async adapt(builder) {
      /* ... */
    },
  };
}
```

```ts
import type { Adapter } from "@sveltejs/kit";

export default function zurichCloud(): Adapter {
  return {
    name: "@sveltejs/adapter-zurich-cloud",
    async adapt(builder) {
      builder.writeClient("dist/client");
      builder.writePrerendered("dist/client");
    },
  };
}
```

```ts {9-10}
import type { Adapter } from "@sveltejs/kit";

export default function zurichCloud(): Adapter {
  return {
    name: "@sveltejs/adapter-zurich-cloud",
    async adapt(builder) {
      builder.writeClient("dist/client");
      builder.writePrerendered("dist/client");
      const serverOutDir = ".zurich";
      builder.writeServer(`${serverOutDir}/server`);
    },
  };
}
```

```ts {11-15|7-15}
import type { Adapter } from "@sveltejs/kit";

export default function zurichCloud(): Adapter {
  return {
    name: "@sveltejs/adapter-zurich-cloud",
    async adapt(builder) {
      builder.writeClient("dist/client");
      builder.writePrerendered("dist/client");
      const serverOutDir = ".zurich";
      builder.writeServer(`${serverOutDir}/server`);
      const manifest = builder.generateManifest({ relativePath: "./server" });
      await writeFile(
        `${serverOutDir}/manifest.mjs`,
        `export const manifest = ${manifest};`,
      );
    },
  };
}
```

```ts
builder.writeClient("dist/client");
builder.writePrerendered("dist/client");
const serverOutDir = ".zurich";
builder.writeServer(`${serverOutDir}/server`);
const manifest = builder.generateManifest({ relativePath: "./server" });
await writeFile(
  `${serverOutDir}/manifest.mjs`,
  `export const manifest = ${manifest};`,
);
```

```ts {10-13}
builder.writeClient("dist/client");
builder.writePrerendered("dist/client");
const serverOutDir = ".zurich";
builder.writeServer(`${serverOutDir}/server`);
const manifest = builder.generateManifest({ relativePath: "./server" });
await writeFile(
  `${serverOutDir}/manifest.mjs`,
  `export const manifest = ${manifest};`,
);
builder.copy(
  fileURLToPath(new URL("./entrypoint.ts", import.meta.url)),
  `${serverOutDir}/functions/entrypoint.ts`,
);
```

```ts
builder.copy(
  fileURLToPath(new URL("./entrypoint.ts", import.meta.url)),
```
````

</div>
<p v-if="$clicks === 3" class="mt-5">SvelteKit inverts control: adapters <em>orchestrate</em> the build rather than hooking into it.</p>
<div v-if="$clicks >= 10" class="svelte-code svelte-handler mt-5">

<!-- prettier-ignore -->
````md magic-move [./entrypoint.ts] {at:11} {duration:700}
```ts
export default (request: Request) => new Response("…");

export const config = {
  path: "/*",
};
```

```ts
import { env } from "node:process";
import { Server } from "../server/index.js"; // SvelteKit server output
import { manifest } from "../manifest.mjs";

const server = new Server(manifest);
await server.init({ env });

export default (request: Request) => new Response("…");

export const config = {
  path: "/*",
};
```

```ts
import { env } from "node:process";
import { Server } from "../server/index.js"; // SvelteKit server output
import { manifest } from "../manifest.mjs";

const server = new Server(manifest);
await server.init({ env });

export default (request: Request) => server.respond(request, {});

export const config = {
  path: "/*",
};
```
````

</div>
</CodeReferenceAccent>
</div>

<style>
h1 { margin-bottom: 16px !important; }
.svelte-code :deep(pre), .svelte-code :deep(code) { line-height: 1.25 !important; }
.svelte-handler { animation: handler-enter 350ms ease both; }
@keyframes handler-enter { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: none; } }
@media (prefers-reduced-motion: reduce) { .svelte-handler { animation: none; } }
</style>

<!--
Start with the user's documented svelte.config.js format. The @sveltejs/adapter-zurich-cloud name is fictional; the APIs are real. Other user settings such as preprocess are omitted.

Click 1: selected Adapter and Builder members, abbreviated from SvelteKit's public types. Optional members such as emulate and supports, additional builder methods, and optional generateManifest routes are omitted.

Click 2: the typed adapter factory with an empty adapt method. SvelteKit invokes it after its build.

Click 3: write browser and prerendered files to dist/client.

Click 4: choose .zurich as our adapter output directory and write SvelteKit's generated server into its server subdirectory. Fade the previous lines. Cleanup and directory setup are omitted.

Click 5: generate and write the manifest beside the server directory. relativePath ./server matches that directory. writeFile is imported from node:fs/promises; its import is omitted from the excerpt.

Click 6: highlight the entire adapt body, fading the surrounding factory.

Click 7: move the adapt body to the top and remove the surrounding boilerplate.

Click 8: copy our entrypoint.ts template directly to .zurich/functions/entrypoint.ts, where ZurichCloud discovers functions. The package ships this template as an asset; its ../server/index.js and ../manifest.mjs imports resolve after copying. fileURLToPath is imported from node:url.

Click 9: collapse to the first two lines of that copy call, keeping the source reference visible.

Click 10: open entrypoint.ts underneath, starting with a basic ZurichCloud Function and catch-all routing config. Accent both mentions of the filename.

Click 11: add SvelteKit's Server and the manifest we just generated, then initialize the server with runtime environment variables.

Click 12: replace the placeholder response with server.respond. Empty response options suffice for this basic page; real platform support also supplies getClientAddress and event.platform.

This covers a minimal SSR page with actual framework and bundler APIs, not every production feature. Native dependencies, server-side file assets/read support, instrumentation, prerendered redirects, and platform-specific routing refinements require more work. No claim that this excerpt replaces the complete Netlify adapter. It has been checked against docs and adapter source, not executed as a SvelteKit deployment.

Sources: https://svelte.dev/docs/kit/writing-adapters ; https://svelte.dev/docs/kit/@sveltejs-kit#Builder ; https://github.com/sveltejs/kit/blob/main/packages/adapter-netlify/index.js
-->

---
level: 2
class: authored
---

# ZurichCloud SvelteKit adapter

<div class="mb-5 flex items-center gap-4">
  <LevelBadge :number="5" class="!mb-0">Full stack</LevelBadge>
  <img src="/astro.svg" alt="Astro" class="w-10 h-10 brightness-0 invert" />
  <SvelteArrival />
</div>

```sh
$ vite build
```

<div class="svelte-build-output">

```text [Build output]
dist/client/         # Publish directory
  _app/              # Browser JS + CSS
  …                  # Static and prerendered files
.zurich/
  functions/
    entrypoint.ts    # ZurichCloud Function
  server/            # SvelteKit server output
  manifest.mjs
```

</div>

<p class="mt-6">Same result as Astro. Whole separate adapter, with a different API.</p>

<style>
h1 { margin-bottom: 16px !important; }
.svelte-build-output :deep(.line:nth-child(-n+3) span) { color: #fcd34d !important; }
.svelte-build-output :deep(.line:nth-child(n+4) span) { color: #67e8f9 !important; }
</style>

<!--
The adapter's build output. ZurichCloud discovers functions in .zurich/functions and packages each entry point with its imported server code, manifest, and dependencies. The adapter does not run esbuild itself. The regular Netlify Functions path in the real SvelteKit adapter follows this division of responsibility; its explicit esbuild step is for Edge Functions. The directory names here remain our fictional platform contract. Static/prerendered files take precedence over the catch-all function.
-->

---
level: 2
class: authored
---

# React Router (Remix)

<div class="absolute right-14 top-10 flex items-center gap-4">
  <LevelBadge :number="5" class="!mb-0">Full stack</LevelBadge>
  <img src="/astro.svg" alt="Astro" class="w-10 h-10 brightness-0 invert" />
  <img src="/svelte.svg" alt="SvelteKit" class="w-10 h-10 brightness-0 invert" />
  <ReactRouterArrival :revealed="$clicks >= 1" />
</div>

<p class="mb-6">No adapter API! It's just Vite. <span v-click="1">Users install our Vite plugin:</span></p>

````md magic-move [vite.config.ts] {at:1} {duration:700}
```ts
import { defineConfig } from "vite";
import { reactRouter } from "@react-router/dev/vite";

export default defineConfig({
  plugins: [reactRouter()],
});
```

```ts {3,6}
import { defineConfig } from "vite";
import { reactRouter } from "@react-router/dev/vite";
import zurich from "@zurich/react-router/vite";

export default defineConfig({
  plugins: [reactRouter(), zurich()],
});
```
````

<div v-click="2" class="mt-4 flex items-center gap-5">
  <img src="/vite.svg" alt="Vite" class="w-14 h-14" />
  <span>The framework and the platform <u>only talk to Vite</u>.</span>
</div>

<p v-click="3" class="mt-6 flex items-start gap-3 text-[#cbd5e1]">
  <svg class="w-6 h-6 shrink-0 mt-1 text-[#bef264]" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
    <path d="M5 4h14a2 2 0 0 1 2 2v10a2 2 0 0 1-2 2H9l-5 3v-3a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2Z" />
    <path d="M7 9h10M7 13h6" />
  </svg>
  <span>But what if they need to talk to each other? More on that soon 👀</span>
</p>

<style>
h1 { margin-bottom: 12px !important; }
.slidev-code-magic-move { --slidev-code-line-height: 1.25; }
</style>

<!--
This is React Router's framework mode, descended from Remix. Its build integration is a Vite plugin.

Click 1: a platform integration can be another Vite plugin. @zurich/react-router/vite is a fictional package showing that arrangement; this isn't a real plugin or a promise about universal plugin ordering. The platform integration arranges the wrapper and platform output.

Click 2: this gives us a different place to do the same work. The common build engine is Vite. What information crosses that boundary matters, and we'll return to that later.

Click 3: tease the later Vite interoperability section, without opening another API walkthrough here. React Router does expose presets, buildEnd, and a build manifest including server bundle information. The distinction here is Netlify's Vite-plugin-only integration, not the absence of all framework-specific APIs.

Philippe's implementation context: today Netlify only supplies a React Router Vite plugin. It cannot control user-defined serverBundles (custom server bundle splitting) through that Vite surface; that information lives in React Router's configuration. Don't imply that React Router itself cannot expose it.

Optional bridge for the later Vite section: custom server bundle splitting is a concrete example of why the platform needs both request entry points and routing information. If the framework exposes those through the shared Vite surface, the platform plugin can consume them without reaching into React Router's config. Keep this as a brief example if time allows; no extra slide or preset detour in the 25-minute talk.

There are also templates that leave the server and platform wiring in the user's project. That makes the platform visible, with the same ownership tradeoff we just discussed. Avoid attributing a blanket anti-abstraction position to the team without a direct source.

Sources: https://api.reactrouter.com/v7/variables/_react-router_dev.vite.reactRouter.html ; https://reactrouter.com/api/framework-conventions/react-router.config.ts ; https://reactrouter.com/how-to/server-bundles
-->

---
level: 2
class: authored
clicks: 3
---

# A unique adapter per framework. Unless...?

<FrameworkDeploymentComparison :step="$clicks" />

<style>
h1 { margin-bottom: 16px !important; }
</style>

<!--
A quick visual recap, about 45–60 seconds, focused on server deployment. Static files are deliberately outside this diagram; we already established that side. These are responsibility diagrams, not precise build timelines.

Compare the two familiar jobs: build the server code, then adapt it for ZurichCloud. Logos inside the boxes identify who does each job. Start with Astro building its server code through Vite and our Astro adapter using Astro's hooks to shape the build and generate platform-specific output.

Click 1: SvelteKit also orchestrates Vite. In both rows the framework wraps Vite, and its platform adapter sits outside that build box. Our adapter uses SvelteKit's Builder API to prepare platform output. These framework-specific integration APIs can still configure or register Vite plugins.

Click 2: the Vite frame now includes our platform plugin. React Router and Netlify's framework-specific Vite plugin participate in that shared build surface. This doesn't imply direct plugin-to-plugin calls or an absence of other React Router APIs. React Router owns its server implementation; Vite is the build integration layer.

Click 3: Nuxt contains Nitro (v2), which contains its builder and our platform preset. The builder label describes its role; Nitro v2 uses Rollup internally. The nested boxes show included components; don't treat them as a precise build timeline. Nuxt still supplies its rendering logic and uses Vite elsewhere; don't imply Nitro builds Nuxt's browser app or replaces its renderer.

Skip another user configuration example here. The next slide explains that Nitro distributes the preset implementations as well. Explicit nitro.preset selection and automatic platform detection can be mentioned verbally if useful.

Sources: https://docs.astro.build/en/reference/adapter-reference/ ; https://svelte.dev/docs/kit/writing-adapters ; https://reactrouter.com/api/framework-conventions/react-router.config.ts ; https://v2.nitro.build/deploy ; https://github.com/nitrojs/nitro/blob/v2/src/presets/netlify/preset.ts
-->

---
level: 2
class: authored
clicks: 8
title: "Nitro: an adapter API and all the adapters"
---

<h1 v-if="$clicks < 3">Nitro: an adapter API <em>and</em> all the adapters</h1>
<h1 v-else>ZurichCloud Nitro preset</h1>

<img v-if="$clicks < 7" src="/nitro.svg" alt="Nitro" class="absolute right-14 top-10 w-12 h-12" />
<FrontendCloudLevel v-else :celebrate="$clicks >= 8">
  <div class="flex items-center gap-4">
  <img src="/astro.svg" alt="Astro" class="w-10 h-10 brightness-0 invert" />
  <img src="/svelte.svg" alt="SvelteKit" class="w-10 h-10 brightness-0 invert" />
  <img src="/reactrouter.svg" alt="React Router" class="w-10 h-10 brightness-0 invert" />
  <NitroArrival />
  <NuxtArrival />
  <AnalogArrival />
  </div>
</FrontendCloudLevel>

<div class="grid gap-9" :class="[$clicks < 3 ? 'grid-cols-2' : 'grid-cols-1', { 'nitro-cleared': $clicks >= 8 }]">
<div class="nitro-presets">

<!-- prettier-ignore -->
````md magic-move [Nitro source] {at:2} {duration:700}
```text
src/presets/
├─ cloudflare/
├─ deno/
├─ netlify/
├─ node/
├─ vercel/
└─ …
```

```text {7-9}
src/presets/
├─ cloudflare/
├─ deno/
├─ netlify/
├─ node/
├─ vercel/
├─ zurich-cloud/
│  ├─ preset.ts
│  └─ runtime/
└─ …
```

```text
zurich-cloud/
├─ preset.ts
└─ runtime/
```
````

</div>
<div v-if="$clicks < 3" class="pt-2">

<p>A framework-agnostic adapter ("preset") API.</p>
<p v-click="1" class="mt-5"><em>And</em> 30+ presets.</p>

</div>
</div>
<div v-if="$clicks >= 4" class="nitro-preset-sketch mt-2" :class="{ 'nitro-cleared': $clicks >= 8 }">

<!-- prettier-ignore -->
````md magic-move [zurich-cloud/preset.ts] {at:5} {duration:700}
```ts
import { defineNitroPreset } from "nitropack/kit";

export default defineNitroPreset({
}, { name: "zurich-cloud", url: import.meta.url });
```

```ts {4}
import { defineNitroPreset } from "nitropack/kit";

export default defineNitroPreset({
  entry: "./runtime/entrypoint",
}, { name: "zurich-cloud", url: import.meta.url });
```

```ts {5-8}
import { defineNitroPreset } from "nitropack/kit";

export default defineNitroPreset({
  entry: "./runtime/entrypoint",
  output: {
    publicDir: "{{ rootDir }}/dist/client",
    serverDir: "{{ rootDir }}/.zurich/functions/ssr",
  },
}, { name: "zurich-cloud", url: import.meta.url });
```

```ts {9-11}
import { defineNitroPreset } from "nitropack/kit";

export default defineNitroPreset({
  entry: "./runtime/entrypoint",
  output: {
    publicDir: "{{ rootDir }}/dist/client",
    serverDir: "{{ rootDir }}/.zurich/functions/ssr",
  },
  hooks: {
    compiled(nitro) { /* Routing, redirects, headers… */ },
  },
}, { name: "zurich-cloud", url: import.meta.url });
```
````

</div>

<style>
h1 { margin-bottom: 16px !important; }
.nitro-presets, .nitro-preset-sketch { --slidev-code-line-height: 1.1; }
.nitro-cleared { opacity: 0; pointer-events: none; transition: opacity 400ms ease; }
@media (prefers-reduced-motion: reduce) { .nitro-cleared { transition: none; } }
</style>

<!--
Nitro defines the preset interface AND distributes target implementations. The selected directories are real Nitro v2 source directories; node is a runtime target, not a hosting company.

Click 1: Nitro ships implementations as well as the API.

Click 2: add and highlight our hypothetical zurich-cloud directory, including preset.ts and runtime/.

Click 3: collapse the other directories and remove the explanatory text, keeping just our preset directory. Change the title to ZurichCloud Nitro preset.

Click 4: open preset.ts below the directory excerpt, starting with defineNitroPreset and the preset's identity. Click 5: add our runtime entry. Click 6: configure the client and server output locations. Click 7: add the compiled hook, fading the previous configuration, and reveal the Level 5 badge with the logo entrances. Click 8: fade out the content below the title, move the badge and logos to the center, then level up to Level 6: Frontend cloud.

This is a sketch using Nitro v2's actual defineNitroPreset API, entry, output, compiled hook, name and url fields. The ZurichCloud target and paths are fictional. url resolves the relative runtime entry; publicDir and serverDir control output locations. Nitro performs the build with these options, then calls compiled. Its body is intentionally omitted: our code would translate routing and static rules into ZurichCloud's format.

runtime/entrypoint supplies the platform request wrapper around Nitro's app. This sketch doesn't include that implementation, generated function configuration, or all production packaging details. It is not a complete deployable preset. The real Netlify preset is the reference for the shape, not a claim that these invented paths match Netlify.

The ability to reuse this implementation across frameworks using Nitro remains the larger point; leave that discussion for the next transition rather than adding more footer copy here.

Sources: https://github.com/nitrojs/nitro/blob/v2/src/presets/_all.gen.ts ; https://github.com/nitrojs/nitro/blob/v2/src/presets/netlify/preset.ts ; https://v2.nitro.build/deploy/custom-presets
-->

---
level: 2
class: authored
clicks: 3
title: Nitro is becoming a Vite plugin
---

<h1>Nitro is becoming a Vite plugin</h1>

<NitroChoiceTransition :step="$clicks">
<template #comparison>

<NitroEvolution :evolved="false" />
<div v-click="1" class="mt-2 leading-tight">TanStack Start and SolidStart no longer include Nitro:</div>
<NitroEvolution v-click="1" :evolved="true" class="mt-2" />

</template>
<template #nitro>

<!-- prettier-ignore -->
```ts [vite.config.ts] {3,6}
import { tanstackStart } from "@tanstack/react-start/plugin/vite";
import react from "@vitejs/plugin-react";
import { nitro } from "nitro/vite";

export default {
  plugins: [tanstackStart(), react(), nitro()],
};
```

</template>
<template #alternative>

<!-- prettier-ignore -->
```ts [vite.config.ts] {3,6}
import { tanstackStart } from "@tanstack/react-start/plugin/vite";
import react from "@vitejs/plugin-react";
import zurich from "@zurich/tanstack-start/vite";

export default {
  plugins: [tanstackStart(), react(), zurich()],
};
```

</template>
</NitroChoiceTransition>

<style>
h1 { margin-bottom: 8px !important; }
</style>

<!--
About 30–45 seconds. Start with the familiar Nuxt diagram: Nuxt includes Nitro v2, and Nitro contains both its builder and our platform preset. The previous slide showed how we implement that preset.

Click 1: reveal the TanStack Start diagram below, keeping the Nuxt/Nitro v2 diagram visible above for comparison. Vite is the outer box in the lower diagram; TanStack Start and Nitro v3 participate as separate plugins. Nitro contains the deployment preset, while the framework sits alongside it. The server label represents build output passing through the shared Vite build, not a direct plugin-to-plugin API.

Click 2: fade out the diagrams, keeping the slide title. Bring “Users install the Nitro Vite plugin” up beneath it. The TanStack Start React configuration appears automatically after the move. Click 3: show the alternative deployment plugin sentence and a second configuration using our fictional ZurichCloud TanStack Start Vite plugin. These are alternatives, not two plugins to install together. The ZurichCloud package name is invented; the Nitro setup follows TanStack's hosting documentation, with Vite's optional defineConfig helper omitted.

TanStack Start removed built-in Nitro, and SolidStart v2 made the same architectural move. Users can choose Nitro or a direct platform deployment plugin, including Netlify and Cloudflare. The point is that Nitro is optional, not that its presets have disappeared. Nuxt remains the v2 example; don't imply Nuxt removed Nitro.

This is a responsibility diagram, not a precise build timeline. Nitro v3 has responsibilities beyond the preset shown here. Don't imply the preset internals are identical between Nitro majors, or that adding Nitro to any arbitrary Vite-based framework automatically works.

Sources: https://github.com/TanStack/router/blob/main/docs/start/framework/react/guide/hosting.md#nitro ; https://docs.solidjs.com/solid-start/v2/guides/deployment-plugins ; https://github.com/solidjs/solid-start/discussions/2281
-->
