---
level: 2
class: authored
---

# Bundlers and frameworks enter the scene

<LevelBadge :number="3">Builds</LevelBadge>

<div class="build-overview">
  <div v-click="1"><strong>Static site generation (SSG):</strong> generate pages at build time.</div>
  <ToolLogos v-click="1" :revealed="$clicks >= 1" :logos="[
    { name: 'Jekyll', src: '/jekyll.svg' },
    { name: 'Hugo', src: '/hugo.svg' },
    { name: 'Gatsby', src: '/gatsby.svg' },
    { name: 'Eleventy', src: '/eleventy.svg' },
    { name: 'Docusaurus', src: '/docusaurus.svg' },
    { name: 'VitePress', src: '/vitepress.svg', color: true },
  ]" />
  <div v-click="2" class="bundling-definition"><strong>Bundling:</strong> package code and assets for the browser.</div>
  <ToolLogos v-click="2" :revealed="$clicks >= 2" :logos="[
    { name: 'Browserify', src: '/browserify.png' },
    { name: 'webpack', src: '/webpack.svg' },
    { name: 'Rollup', src: '/rollupdotjs.svg' },
    { name: 'esbuild', src: '/esbuild.svg' },
    { name: 'Vite', src: '/vite.svg', color: true },
  ]" />
  <div v-click="3" class="framework-aside">
    <svg class="aside-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
      <path d="M5 4h14a2 2 0 0 1 2 2v10a2 2 0 0 1-2 2H9l-5 3v-3a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2Z" />
      <path d="M7 9h10M7 13h6" />
    </svg>
    <div>
      <div>The user might use a single-page app (SPA) framework like React or Vue.</div>
      <div>But ZurichCloud doesn't actually care about that.</div>
    </div>
  </div>
</div>
<style>
h1 { margin-bottom: 12px !important; }
h2 { margin-bottom: 12px !important; }
.build-overview { margin-top: 22px; line-height: 1.35; }
.bundling-definition { margin-top: 42px; }
.framework-aside {
  display: flex;
  align-items: flex-start;
  gap: 14px;
  margin-top: 28px;
  padding: 12px 16px;
  border-radius: 8px;
  background: #1b2018;
  color: #cbd5e1;
  font-size: 22px;
}
.aside-icon { flex: 0 0 24px; width: 24px; height: 24px; margin-top: 3px; color: #bef264; }
</style>

<!--
- SSG ≠ just Markdown. Bundling ≠ just components.
- Static output: no framework-specific serving logic.
-->

---
level: 2
class: authored build-deploy-slide
---

# Configurable build command

<LevelBadge :number="3">Builds</LevelBadge>

<div class="build-instruction">The user tells us how to build their site:</div>

<div class="build-details">
<CodeBlockWrapper v-click="1" title="zurich.json">
<pre class="slidev-code"><code>{
  <span class="build-existing">"name": "hello",</span>
<span class="build-command-line" :class="{ shown: $clicks >= 2 }" :aria-hidden="$clicks < 2">  <span class="build-command">"build_command"</span>: "<span class="build-command">hugo build</span>",</span>  <span class="build-directory">"publish_dir"</span>: "<span class="build-directory">dist/</span>"
}</code></pre>
</CodeBlockWrapper>

<div v-click="2" class="build-project">
  <div class="build-run"><code><span class="build-prompt" aria-hidden="true">$ </span>hugo build</code><span aria-hidden="true">↓</span></div>
  <pre class="build-tree"><code><span class="build-output" :class="{ generated: $clicks >= 3 }" :aria-hidden="$clicks < 3"><span class="build-directory">dist/</span>
  ├─ <span :class="{ 'text-fuchsia-300': $clicks >= 4 }">about.html</span>
  └─ styles.css</span><span class="build-source">hugo.toml
package.json
src/
  └─ index.md</span></code></pre>
</div>
</div>

<div v-click="4" class="build-result">
  <div class="build-url"><code>https://hello.zurich.cloud/<span class="text-fuchsia-300">about</span></code></div>
</div>

<Achievement v-click="5">Congratulations, you've built a clone of Netlify, c. 2015!</Achievement>

<style>
h1 { margin-bottom: 12px !important; }
h2 { margin-bottom: 12px !important; }
.build-instruction { margin-bottom: 16px; }
.build-details { display: grid; grid-template-columns: 1fr 1fr; gap: 32px; align-items: center; }
.build-details pre { line-height: 1.35; }
.build-command { color: #67e8f9; }
.build-directory { color: #fcd34d; }
.build-existing { color: #94a3b8; }
.build-command-line { display: block; max-height: 0; opacity: 0; overflow: hidden; transition: max-height 500ms ease, opacity 500ms ease; }
.build-command-line.shown { max-height: 1.5em; opacity: 1; }
@media (prefers-reduced-motion: reduce) { .build-command-line { transition: none; } }
.build-project { min-height: 196px; }
.build-run { display: flex; align-items: center; justify-content: space-between; padding: 4px 14px; border: 2px solid #67e8f9; border-radius: 10px; background: #132a32; color: #67e8f9; }
.build-run code { font-size: 22px; color: inherit; background: transparent; }
.build-prompt { color: #94a3b8; }
.build-tree { margin: 10px 0 0; padding: 0 14px !important; border-left: 2px solid #45552c; background: #191d17 !important; font-size: 18px; line-height: 22px !important; }
.build-tree code { font-size: inherit; line-height: inherit; }
.build-source { color: #cbd5e1; }
.build-output { display: block; max-height: 0; overflow: hidden; opacity: 0; transform: translateY(-8px); transition: max-height 600ms ease, opacity 400ms ease, transform 600ms ease; }
.build-output.generated { max-height: 66px; opacity: 1; transform: translateY(0); }
@media (prefers-reduced-motion: reduce) { .build-output { transition: none; } }
.build-result { display: flex; align-items: center; gap: 20px; margin-top: 12px; }
.build-url { display: flex; align-items: center; gap: 20px; }
.build-url code { font-size: 24px; }
.achievement { margin-top: 16px; }
</style>

<!--
- Assume Hugo is configured to output to dist/.
-->

---
level: 2
class: authored
---

# Users don't want to configure stuff

<LevelBadge :number="4">Zero config</LevelBadge>

<div class="detection-examples">
<div class="detection-inputs">
<div v-click="1" class="detection-package">

```json [package.json]
{
  "devDependencies": {
    "vite": "^7.0.0"
  }
}
```

<img src="/vite.svg" alt="Vite" />
</div>
<div v-click="2" class="detection-file"><code>turbo.json</code><img class="detection-mono" src="/turborepo.svg" alt="Turborepo" /></div>
<div v-click="3" class="detection-file"><code>pnpm-lock.yaml</code><img class="detection-mono" src="/pnpm.svg" alt="pnpm" /></div>
</div>
<div v-click="1" class="detection-arrow">→</div>
<div v-click="1" class="detection-result">
<div class="detected-setting">Build command</div>

````md magic-move {at:2} {duration:700}
```sh
vite build
```
```sh
turbo run build
```
```sh
pnpm exec turbo run build
```
````

<div class="detected-setting detection-output">Output directory <code class="detected-directory">dist/</code></div>
<div v-click="3" class="detected-setting detection-install">Install dependencies <code>pnpm install</code></div>
</div>

</div>

<Achievement v-click="4">Congratulations, you've caught up to Vercel's predecessor ZEIT Now, c. 2019!</Achievement>

<style>
h1 { margin-bottom: 8px !important; }
h2 { margin-bottom: 12px !important; }
.detection-examples { --slidev-code-line-height: 1.2; display: grid; grid-template-columns: 350px 42px 1fr; gap: 24px; align-items: center; }
.detection-inputs { display: grid; gap: 10px; }
.detection-package { position: relative; }
.detection-package > img { position: absolute; right: 14px; top: 12px; }
.detection-inputs img { width: 30px; height: 30px; object-fit: contain; }
.detection-examples :deep(pre code) { line-height: 1.2 !important; }
.detection-examples :deep(pre) { padding: 8px !important; }
.detection-arrow { color: #94a3b8; font-size: 28px; text-align: center; }
.detection-file { display: flex; align-items: center; justify-content: space-between; padding: 10px 14px; border: 1px solid #64748b; border-radius: 8px; background: #17202e; }
.detection-file code { font-size: 22px; background: transparent; }
.detection-mono { filter: brightness(0) invert(1); }
.detected-setting { font-size: 22px; line-height: 1.3; }
.detection-result > .detected-setting:first-child { margin-bottom: 10px; }
.detection-output, .detection-install { margin-top: 18px; }
.detection-output code, .detection-install code { display: block; }
.detected-setting code { display: inline-block; margin-top: 6px; font-size: 18px; white-space: nowrap; }
.detected-command { color: #67e8f9; }
.detected-directory { color: #fcd34d; }
</style>

<!--
- Vite → vite build + dist/. Turbo → turbo run build. pnpm → pnpm exec turbo run build.
- Package manager also determines the install command.
- Infer defaults; explicit user settings win.
-->
