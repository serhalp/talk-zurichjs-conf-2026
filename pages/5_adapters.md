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
- We made deployment glue the user’s problem.
- Framework differences × version differences.
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
- Ship fixes centrally. Users update and rebuild.
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
- config:setup: merge settings before config is finalized.
- config:done: resolved config; register the adapter.
- serverEntrypoint = our input module.
- build.server + serverEntry = output directory + filename.
- ssr.noExternal: bundle JS dependencies.
- astro/app/entrypoint: createApp() → app.render(Request) → Response.
- Forward Astro’s Set-Cookie headers.
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
- Remember the copy-paste problem? User already told Astro.
- Static headers: opt in with adapterFeatures.staticHeaders; read routeToHeaders.
- No function runs when a prerendered file is served.
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
- Astro emits the function entry; platform packages its dependencies.
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
- SvelteKit calls adapt() after its build.
- Adapter orchestrates output via Builder; Astro uses hooks.
- Manifest connects routes to generated server code.
- Copy our template → initialize Server → respond(request).
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
- Platform packages Function dependencies.
- Explicit esbuild step in the real adapter is for Edge Functions.
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
- RR does have presets/build hooks. Netlify uses only a Vite plugin.
- Custom serverBundles live in RR config; our plugin can’t control them.
- Callback later: entry points + routing.
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
- Responsibility diagrams, not build timelines.
- Nuxt supplies rendering; Nitro supplies server tooling + deployment presets.
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
- One preset reusable across Nitro-based frameworks.
- entry = platform wrapper; output = build destinations.
- compiled hook: emit platform routing/config.
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
- TanStack Start + SolidStart removed built-in Nitro.
- Users choose Nitro or a direct platform plugin.
- Nuxt still includes Nitro.
-->
