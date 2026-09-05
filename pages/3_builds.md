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
[Finish section 1 within about 3 minutes total. The level reveals should move quickly.]

Users don't want to hand-code every page or copy the same navigation into fifty HTML files. They want to write Markdown, reuse templates, or build with components. These tools let them do that, but the source in their repo isn't the website we can serve yet.

Click 1 introduces SSG and reveals its logos in sequence. Click 2 introduces bundling and reveals its logos in sequence. These are examples of capabilities, not exclusive categories: Gatsby does more than SSG, and Vite is a broader build tool.

Click 3: the app may use React or Vue. ZurichCloud does not need a framework-specific integration to serve the static build output.
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
The user tells us how to build their site. Click 1 shows name and publish_dir. Click 2 inserts build_command above publish_dir as the command appears in the diagram. The command is cyan; the output directory is amber throughout.

Click 2: ZurichCloud runs hugo build. Click 3: dist/ and its generated files animate into their alphabetical position above hugo.toml, package.json, and src/. Hugo writes the generated site into dist/. The user can push their source instead of building and uploading it themselves. We use dist/ as the illustrative output directory for this talk; assume Hugo is configured to write there.

Click 4: ZurichCloud serves those generated files at the same site URL. The URL maps to dist/about.html, a generated page in this illustrative project. We still end up uploading files to the CDN; we don't need a framework-specific serving integration.

The redirects, rewrites, and headers from the previous slides still work; they're omitted here to focus on the build settings.

Click 5: this is roughly the original Netlify idea. Its March 31, 2015 launch was titled “Builds, Deploys and Hosts Your Static Site or App.” This is a conceptual milestone, not an exhaustive recreation of that product.

Sources: https://news.ycombinator.com/item?id=9297316 and https://gohugo.io/getting-started/usage/
-->

---
level: 2
class: authored
---

# Users don't want to configure stuff

<LevelBadge :number="4">Zero config</LevelBadge>

<div class="detection-examples">
<div v-click="1" class="detection-file"><code>pnpm-lock.yaml</code></div>
<div v-click="1" class="detection-arrow">→</div>
<div v-click="1" class="detected-tool"><img class="detection-mono" src="/pnpm.svg" alt="">pnpm</div>
<div v-click="1" class="detection-arrow">→</div>
<div v-click="1" class="detected-setting"><div>Install dependencies</div><code>pnpm install</code></div>

<div v-click="2" class="detection-file"><code>turbo.json</code></div>
<div v-click="2" class="detection-arrow">→</div>
<div v-click="2" class="detected-tool"><img class="detection-mono" src="/turborepo.svg" alt="">Turborepo</div>
<div v-click="2" class="detection-arrow">→</div>
<div v-click="2" class="detected-setting"><div>Build command</div><code class="detected-command">pnpm exec turbo build</code></div>

<div v-click="3">

```json [package.json]
{
  "devDependencies": {
    "vite": "^7.0.0"
  }
}
```

</div>
<div v-click="3" class="detection-arrow">→</div>
<div v-click="3" class="detected-tool"><img src="/vite.svg" alt="">Vite</div>
<div v-click="3" class="detection-arrow">→</div>
<div v-click="3" class="detected-setting"><div>Output directory</div><code class="detected-directory">dist/</code></div>

</div>

<Achievement v-click="4">Congratulations, you've caught up to Vercel's predecessor ZEIT Now, c. 2019!</Achievement>

<style>
h1 { margin-bottom: 8px !important; }
h2 { margin-bottom: 12px !important; }
.detection-examples { --slidev-code-line-height: 1.2; display: grid; grid-template-columns: 300px 24px 190px 24px 1fr; column-gap: 12px; row-gap: 8px; align-items: center; }
.detection-examples :deep(pre code) { line-height: 1.2 !important; }
.detection-examples :deep(pre) { padding: 8px !important; }
.detection-arrow { color: #94a3b8; font-size: 28px; text-align: center; }
.detection-file { padding: 10px 14px; border-left: 2px solid #45552c; background: #191d17; }
.detection-file code { font-size: 22px; background: transparent; }
.detected-tool { display: flex; align-items: center; gap: 12px; font-size: 24px; }
.detected-tool img { width: 32px; height: 32px; object-fit: contain; }
.detection-mono { filter: brightness(0) invert(1); }
.detected-setting { font-size: 22px; line-height: 1.3; }
.detected-setting code { display: inline-block; margin-top: 6px; font-size: 18px; white-space: nowrap; }
.detected-command { color: #67e8f9; }
.detected-directory { color: #fcd34d; }
</style>

<!--
[Keep this brief: one more capability before server rendering.]

The user doesn't want to manually configure things we can infer. Instead of listing every category of tool, show three concrete clues and what each helps us decide.

Click 1: pnpm-lock.yaml suggests pnpm. We need to install the user's dependencies before building, so this also gives us an install command. Exact CI flags, package-manager version selection, and conflicting lockfiles are outside this sketch.

Click 2: turbo.json suggests Turborepo. In this illustrative pnpm workspace with a configured build task, pnpm exec turbo build runs that task. The filename alone does not prove that task exists or select which workspace to deploy; a real implementation inspects the configuration and workspace layout too.

Click 3: the actual devDependencies object in package.json contains Vite and its version range. This suggests a default dist output directory. It is an excerpt, not the whole package.json. The range is illustrative; detection can use resolved versions when available and must account for user overrides such as build.outDir.

Click 4: the milestone refers to basic automatic framework defaults, not the dates when these specific modern tools were supported. Netlify was demonstrably prefilling Gatsby settings by February 2019; ZEIT Now announced Zero Config Deployments in August 2019. This is not a claim about who invented detection first. Sources: https://dev.to/imshuffling_31/deploying-your-gatsbyjs-site-to-netlify-4la and https://vercel.com/blog/zero-config

Combine these clues to infer defaults; let explicit user settings win. This is build configuration detection, separate from adapting a framework's server output later. Other frameworks, bundlers, package managers, monorepo tools, and task runners provide other clues.
-->
