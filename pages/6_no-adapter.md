---
class: authored
clicks: 1
---

# There's always a deployment adapter API, right?

<div class="missing-adapter">
  <div class="framework next">
    <img src="/nextjs.svg" alt="" />
    <span>Next.js</span>
  </div>
  <div class="framework angular">
    <img src="/angular.svg" alt="" />
    <span>Angular</span>
  </div>
  <Transition name="travolta">
    <div v-if="$clicks === 0" class="searching">
      <div class="question">Adapter API?</div>
      <img src="/confused-travolta.gif" alt="Confused John Travolta looking left and right for an adapter API" />
    </div>
  </Transition>
  <div v-click="1" class="answer">
    <span>There's really only one option...</span>
    <span>Run the build, then transform the output.</span>
  </div>
  <img v-if="$clicks >= 1" src="/only-option-cat.png" alt="Wide-eyed cat" class="only-option-cat" />
</div>

<style>
.missing-adapter { position: relative; height: 380px; margin-top: 20px; }
.framework { position: absolute; top: 80px; display: flex; flex-direction: column; align-items: center; gap: 18px; font-size: 30px; }
.framework img { width: 90px; height: 90px; filter: brightness(0) invert(1); }
.next { left: 60px; }
.angular { right: 60px; }
.searching { position: absolute; inset: 0; }
.searching img { position: absolute; width: 600px; max-width: none; left: 50%; bottom: 0; transform: translateX(-50%); }
.question { position: absolute; top: 8px; left: 50%; transform: translateX(-50%); padding: 10px 20px; border: 1px solid #94a3b8; border-radius: 14px; font-size: 28px; }
.answer { position: absolute; inset: 230px 0 auto; display: flex; flex-direction: column; align-items: center; gap: 12px; font-size: 30px; }
.only-option-cat { position: absolute; top: 90px; left: 50%; transform: translateX(-50%); width: 120px; border-radius: 6px; }
.travolta-leave-active { transition: opacity 350ms ease; }
.travolta-leave-to { opacity: 0; }
@media (prefers-reduced-motion: reduce) {
  .travolta-leave-active { transition: none; }
}
</style>

<!--
The transition into adapting build output after the fact. Pause for Travolta to look between Next.js on the left and Angular on the right. Click 1: Travolta and the question disappear; reveal the fallback text and the small cat, which stay visible until the next slide.

This introduces the historical problem that led to the Next.js adapter work later in the talk. Do not claim Next.js still has no deployment adapter API today. Angular and Next.js are the two examples from our platform integration experience, not an exhaustive list or a claim that they have equal complexity.

With no suitable deployment adapter API, we inspect the generated files and wrap, move, or transform them into the platform's deployment format. The next slide can explain the maintenance burden of relying on implementation details.

The GIF is bundled locally for offline presentation. Source: https://knowyourmeme.com/photos/1043243-confused-travolta (transparent Confused Travolta GIF).
-->

---
level: 2
class: authored
clicks: 18
---

# Next.js: build first, "adapt" later

<img src="/nextjs.svg" alt="Next.js" class="absolute right-14 top-10 w-12 h-12 brightness-0 invert" />

<NextOutputWalkthrough>
<div v-if="$clicks <= 1" key="diagram" class="next-pipeline-stage">
  <NextOutputPipeline />
  <div v-click="1" class="pipeline-callout">
    <svg class="w-6 h-6 shrink-0" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
      <path d="M5 4h14a2 2 0 0 1 2 2v10a2 2 0 0 1-2 2H9l-5 3v-3a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2Z" />
      <path d="M7 9h10M7 13h6" />
    </svg>
    <span>This is a whole other talk though...</span>
  </div>
</div>
<div v-else-if="[2, 3, 5, 6].includes($clicks)" key="listing" class="next-directory">

<!-- prettier-ignore -->
```text [Build output] {all|2|all|all|7} {at:3}
.next/
├─ prerender-manifest.json
├─ required-server-files.json
├─ routes-manifest.json
├─ server/
│  ├─ app/
│  ├─ middleware-manifest.json
│  └─ …
├─ static/
└─ …
```

</div>

<div v-else key="preview" class="next-manifest-layout" :class="{ 'minimal-mode-show': $clicks === 13 }">
<div class="manifest-preview">
<Transition name="manifest-step" mode="out-in">
<div v-if="$clicks === 4" key="prerender">

<!-- prettier-ignore -->
```json [prerender-manifest.json] {4-6}
{
  "routes": {
    "/about": {
      "initialRevalidateSeconds": 60,
      "srcRoute": null,
      "dataRoute": "/about.rsc"
    }
  }
}
```

</div>
<div v-else-if="$clicks >= 14" key="output-tree">

<!-- prettier-ignore -->
```text [Build output]
.next/
├─ prerender-manifest.json
├─ required-server-files.json
├─ routes-manifest.json
├─ server/
│  ├─ app/
│  ├─ middleware-manifest.json
│  └─ …
├─ static/
└─ …
```

</div>
<div v-else key="middleware">

<!-- prettier-ignore -->
````md magic-move [server/middleware-manifest.json] {at:9} {duration:700}
```json {5}
{
  "middleware": {
    "/": {
      "matchers": [
        { "regexp": "^/about(?:/.*)?$" }
      ]
    }
  }
}
```

```json {5}
{
  "middleware": {
    "/": {
      "matchers": [
        { "regexp": "(?!.*)" }
      ]
    }
  }
}
```
````

</div>
</Transition>
</div>
<div class="manifest-explanation">
  <template v-if="$clicks === 4">
    <p>Reverse-engineer the types and semantics of every field. <img src="/only-option-cat.png" alt="" class="manifest-cat" /></p>
    <p>Parse the manifest file.</p>
    <p>Translate each prerendered page's metadata to a format ZurichCloud expects.</p>
  </template>
  <template v-else-if="$clicks === 7 || $clicks === 8">
    <p>Reverse-engineer the types and semantics of every field. Again. <img src="/only-option-cat.png" alt="" class="manifest-cat" /></p>
    <p>Parse the manifest file.</p>
    <p>Translate its matchers into routing rules for ZurichCloud Edge Functions.</p>
    <div v-click="8" class="edge-thought">
      <svg viewBox="0 0 100 100" aria-hidden="true">
        <path d="M5 90Q85 85 85 8m-7 10 7-10 7 10" />
      </svg>
      Oh yeah, your platform needs Edge Functions now
    </div>
  </template>
  <template v-else-if="$clicks >= 9 && $clicks <= 13">
    <p>Then mutate the manifest on disk</p>
    <p v-click="10">to prevent the Next.js server from running middleware twice</p>
    <p v-click="11">because this build was meant for standalone Node.js servers</p>
    <p v-click="12">but ZurichCloud is a serverless platform.</p>
  </template>
  <template v-else>
    <p>Private implementation details</p>
    <p v-click="15">No documented contract</p>
    <p v-click="16">No types, no schemas</p>
    <p v-click="17">No SemVer guarantees. Can change at any time.</p>
    <p v-click="18">... and you'll need branching logic to keep supporting every variation indefinitely.</p>
  </template>
</div>
<div v-if="$clicks >= 9 && $clicks <= 13" v-click="13" class="serverless-aside">
  <p>Oh, there's a secret, even less documented mode for <em>a</em> serverless platform, but you <em>really</em> don't want to go there.</p>
  <img v-if="$clicks === 13" src="/war-flashback-dog.gif" alt="Stains the dog having war flashbacks" class="war-flashback-dog" />
</div>
<img v-if="$clicks === 13" src="/next-minimal-mode.png" alt="Next.js source sets minimalMode from minimalMode or process.env.NEXT_PRIVATE_MINIMAL_MODE" class="minimal-mode-source" />
</div>
</NextOutputWalkthrough>

<style>
h1 { margin-bottom: 12px !important; }
.next-pipeline-stage { position: relative; padding-top: 20px; }
.pipeline-callout { position: absolute; left: 124px; bottom: 36px; display: flex; align-items: center; gap: 12px; color: #cbd5e1; }
.pipeline-callout svg { color: #bef264; }
.next-directory { width: 620px; margin: 24px auto 0; }
.next-directory :deep(pre), .next-directory :deep(code) { line-height: 1.4 !important; }
.next-manifest-layout { position: relative; display: grid; grid-template-columns: 1.15fr 1fr; gap: 28px; }
.next-manifest-layout { padding-top: 36px; }
.manifest-preview { --slidev-code-line-height: 1.15; }
.manifest-preview :deep(pre), .manifest-preview :deep(code) { line-height: 1.15 !important; }
.manifest-explanation { padding-top: 8px; line-height: 1.3; }
.manifest-explanation p { margin: 0 0 16px; }
.serverless-aside { grid-column: 1 / -1; display: flex; align-items: center; gap: 24px; width: 800px; margin: 0 auto; color: #cbd5e1; line-height: 1.3; }
.serverless-aside p { flex: 1; margin: 0; border-left: 2px solid #94a3b8; padding-left: 16px; }
.war-flashback-dog { width: 100px; flex-shrink: 0; border-radius: 6px; }
.minimal-mode-show { padding-top: 0; row-gap: 10px; }
.minimal-mode-show .manifest-explanation p { margin-bottom: 8px; }
.minimal-mode-show .war-flashback-dog { width: 72px; }
.minimal-mode-source { grid-column: 1 / -1; width: 800px; margin: 0 auto; border-radius: 6px; }
.edge-thought { position: absolute; top: 320px; left: 48px; width: 390px; padding: 14px 20px; border: 2px solid #94a3b8; border-radius: 32px; background: #17202e; line-height: 1.25; }
.edge-thought svg { position: absolute; left: 100%; top: -80px; width: 100px; height: 100px; overflow: visible; fill: none; stroke: #94a3b8; stroke-width: 1.5; stroke-linecap: round; stroke-linejoin: round; }
.manifest-cat { display: inline-block; width: 36px; margin-left: 4px; vertical-align: middle; border-radius: 3px; opacity: 0; animation: manifest-cat-peek 10s 5s ease-in-out infinite; }
@keyframes manifest-cat-peek {
  0%, 55%, 100% { opacity: 0; }
  5%, 50% { opacity: 1; }
}
.manifest-explanation .manifest-aside { border-left: 2px solid #94a3b8; padding-left: 14px; color: #cbd5e1; }
.manifest-step-enter-active, .manifest-step-leave-active { transition: opacity 300ms ease, transform 300ms ease; }
.manifest-step-enter-from { opacity: 0; transform: translateY(10px); }
.manifest-step-leave-to { opacity: 0; transform: translateY(-10px); }
@media (prefers-reduced-motion: reduce) {
  .manifest-step-enter-active, .manifest-step-leave-active { transition: none; }
}
</style>

<!--
About 60–90 seconds. Grounded in the adjacent next-runtime checkout at 3feea0c7, package @netlify/plugin-nextjs 5.15.12. This is the existing build-output integration, not a statement about whether a new adapter API exists today. Don't spoil that later story on the slide.

Start with the diagram only. It shows next build producing .next/, then our platform build plugin reading and transforming it into static assets, functions, edge functions, redirects, headers, Image CDN configuration, and blobs. The real Netlify plugin sets NEXT_PRIVATE_STANDALONE in onPreBuild; its onBuild copies assets and prerendered content, creates server and edge handlers, and configures headers and images. The diagram describes the deployment responsibilities of our fictional platform integration, not an exact list of Netlify output files: some routing and redirects are handled by the Next.js server at runtime. This is a platform build hook, not a Next.js deployment hook.

Click 1: reveal "This is a whole other talk though...". Click 2: carry .next/ from the diagram into the directory listing. Click 3: highlight prerender-manifest.json. Click 4: hide the listing and open that manifest. Click 5: return to the listing. Click 6: highlight server/middleware-manifest.json. Click 7: hide the listing and open it. Click 8: reveal the Edge Functions thought bubble. Click 9: mutate its matcher on disk. Click 10: explain preventing the Next.js server from running middleware twice. Click 11: explain the standalone Node.js target. Click 12: "but ZurichCloud is a serverless platform." Click 13: the less-documented serverless mode and war-flashback dog. Click 14: explain the private contract and versioning costs.

Both JSON previews are selected fields with illustrative /about values, not complete manifests or captured build output. The shapes and fields come from what the real integration consumes. Additional version, route, runtime, and file metadata is omitted.

Clicks 15–18 reveal the remaining maintenance costs one at a time. The iceberg and congratulations now follow the build-plugin slide as their own slide.

The first preview is prerender-manifest.json. plugin-context.ts reads it directly. content/prerendered.ts reads initialRevalidateSeconds, src/data route information, and HTML/RSC/metadata files to construct cache entries for upload. We must understand the runtime meaning, not just parse JSON. Don't teach ISR here; the 60 is background revalidation information, not a generic CDN TTL.

The second preview is middleware-manifest.json. functions/edge.ts reads the middleware definitions, translates matchers into platform routing patterns, and creates middleware handlers. The sample regexp is illustrative; the field and nested structure are real.

The rewrite: content/server.ts's replaceMiddlewareManifest rewrites every matcher regexp to (?!.*) in the server copy. Middleware runs separately, so this prevents running it twice while retaining other middleware-dependent Next.js behavior. We leave the rest of the manifest intact. This is an actual transformation, not invented toy logic.

The "secret" mode aside refers to minimal mode in the historical integration story; keep this as a quick aside, not a detour into its implementation. Dog GIF supplied by Philippe (fetchpik.com-LBCGVvKWNR.gif), embedded locally for offline playback.

Finally: these are private-ish implementation details, not a documented deployment contract with semver protection. Do not claim Next.js's public APIs ignore semver or that every emitted file is undocumented. The maintenance cost is visible in this checkout: content/prerendered.ts branches on Next.js versions for PAGE/APP_PAGE and PAGE/PAGES/APP_ROUTE cache formats; content/server.ts also applies version-bounded internal module replacements. Those examples establish version coupling, not proof that every minor/patch release breaks the adapter.

Emphasize the implicit versioning: knowing a manifest's explicit version isn't necessarily enough to know how all its fields and associated runtime behavior should be interpreted. We also check the Next.js package version and accommodate changes in generated files and cache formats.

Possible follow-up asset: Philippe records a short scroll through the OpenNext Netlify adapter, pausing on the version ranges, cache-format branches, manifest rewrites, and internal module patches. Use this after the readable example so the audience knows what the scrolling code represents. Embed the recording locally; don't expect the audience to read every line. No recording added yet.

Source pointers in ../next-runtime: src/index.ts onPreBuild/onBuild; src/build/plugin-context.ts getPrerenderManifest/getMiddlewareManifest; src/build/content/prerendered.ts prerenderManifestRouteToRevalidateAndCacheControlProperties/copyPrerenderedContent; src/build/functions/edge.ts buildHandlerDefinition/createEdgeHandlers; src/build/content/server.ts replaceMiddlewareManifest/getPatchesToApply.

Public source: https://github.com/opennextjs/opennextjs-netlify/tree/3feea0c7/src
-->

---
level: 2
class: authored
clicks: 3
---

# Wait, how do we run this stuff after each build?

<Transition name="build-plugin-step" mode="out-in">
<div v-if="$clicks === 0" key="realization" class="build-plugin-realization">
  Oh yeah, your platform needs its own build plugin mechanism.
</div>
<div v-else key="implementation" class="build-plugin-implementation">
  <PlatformBuildLifecycle />

<div v-click="2" class="build-plugin-code">

<!-- prettier-ignore -->
```ts [@zurich/nextjs/index.ts]
import { transformNextOutput } from "./transform-next-output";

export async function onBuild() {
  await transformNextOutput(".next/");
}
```

</div>

<div v-click="3" class="build-plugin-detection">
  <img src="/nextjs.svg" alt="Next.js" class="w-8 h-8 brightness-0 invert" />
  <span><span class="detected-framework">Detect Next.js.<span class="detection-reminder"><svg viewBox="0 0 140 62" aria-hidden="true"><path d="M90 50Q25 50 25 5m-5 8 5-8 5 8" /></svg>Luckily, ZurichCloud already does this!</span></span> Run our plugin automatically.</span>
</div>
</div>
</Transition>

<style>
h1 { margin-bottom: 18px !important; }
.build-plugin-realization { width: 640px; margin: 70px auto 0; border: 2px solid #94a3b8; border-radius: 32px; background: #17202e; padding: 24px 32px; font-size: 28px; line-height: 1.3; }
.build-plugin-code { width: 720px; margin: 12px auto 0; }
.build-plugin-code :deep(pre), .build-plugin-code :deep(code) { line-height: 1.15 !important; }
.build-plugin-detection { display: flex; align-items: center; justify-content: center; gap: 14px; margin-top: 18px; }
.detected-framework { position: relative; display: inline-block; }
.detection-reminder { position: absolute; top: calc(100% + 34px); left: 150px; width: max-content; color: #cbd5e1; }
.detection-reminder svg { position: absolute; left: -100px; top: -34px; width: 140px; height: 62px; fill: none; stroke: #94a3b8; stroke-width: 1.5; stroke-linecap: round; stroke-linejoin: round; }
.build-plugin-step-enter-active, .build-plugin-step-leave-active { transition: opacity 350ms ease; }
.build-plugin-step-enter-from, .build-plugin-step-leave-to { opacity: 0; }
@media (prefers-reduced-motion: reduce) { .build-plugin-step-enter-active, .build-plugin-step-leave-active { transition: none; } }
</style>

<!--
About 30–45 seconds. Keep this about the platform integration mechanism, not a Netlify product tutorial.

Start with the thought bubble. We have written all this code to interpret and transform Next.js output, but something still has to invoke it on every build.

Click 1: ZurichCloud owns the build pipeline. Run the user's build command, run our integration after that command succeeds, then deploy the prepared output. These hooks belong to the platform's build system. They are not Next.js deployment hooks or Vite plugin hooks.

Click 2: package the transformation work from the previous slide as a build plugin. The onBuild export is grounded in the existing Netlify integration at ../next-runtime/src/index.ts: that hook runs after the framework build and prepares static assets, prerendered content, server and edge handlers, headers, and image configuration. @zurich/nextjs and transformNextOutput are fictional names compressing the work we just explored; this is a sketch of the lifecycle, not an executable Netlify plugin. Real implementations also have hooks before the build, for example to select standalone output and restore caches. Skip those details here.

Click 3: remember zero config? Detect Next.js and select/install/run our integration automatically, so users don't have to wire this up themselves. Framework detection is separate from invoking the hook. It chooses which plugin to run; the build pipeline decides when to run it. This makes the experience automatic for users while leaving the integration maintenance with our frameworks team.

The diagram omits install, caching, packaging, and other lifecycle steps. Its purpose is the placement of the post-build integration between the framework build and deployment.
-->

---
level: 2
class: authored
clicks: 2
---

# Next.js: build first, "adapt" later

<div class="next-iceberg-stage">
  <NextIceberg class="compact-iceberg" />
  <div class="iceberg-level">
    <NextHardModeLevel :visible="$clicks >= 2" />
  </div>
  <div v-click="1" class="iceberg-congratulations">
    Congratulations, you've doubled the size of your frameworks team
  </div>
</div>

<style>
h1 { margin-bottom: 12px !important; }
.compact-iceberg { display: block; width: 560px; margin: 0 auto; }
.iceberg-congratulations { width: 780px; margin: 24px auto 0; padding: 10px 24px; border: 2px solid #94a3b8; border-radius: 28px; background: #17202e; color: #f8fafc; font-size: 28px; line-height: 1.25; text-align: center; }
.iceberg-level { display: flex; justify-content: center; margin-top: 18px; min-height: 38px; }
</style>

<!--
We've shown some of the output transformations and how the platform runs them after every build. We've only just begun to scratch the surface.

Click 1: Congratulations, you've doubled the size of your frameworks team.
Click 2: reveal the Level 6 badge above the congratulations. One second after its entry animation finishes, level up to 7: Frontend cloud, hard mode. Keep the iceberg and congratulations visible.

This closes the maintenance story before the OpenNext collaboration: we weren't the only ones doing this.
-->
