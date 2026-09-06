---
class: authored
---

# Let's build... ZurichCloud

<LevelBadge :number="1">Static</LevelBadge>

<svg viewBox="0 0 860 170" class="w-full h-42 my-4 text-slate-200" role="img" aria-label="A Git repo containing static files is uploaded to ZurichCloud's CDN, which serves a browser">
  <rect x="2" y="4" width="224" height="162" rx="12" fill="#17202e" stroke="#94a3b8" stroke-width="2" />
  <image href="/git.svg" x="36" y="15" width="30" height="30" />
  <text x="136" y="40" text-anchor="middle" fill="currentColor" style="font-size: 26px">Git repo</text>
  <g v-click="1" fill="#fcd34d" font-family="monospace" style="font-size: 22px">
    <text x="30" y="80">index.html</text>
    <text x="30" y="114">styles.css</text>
    <text x="30" y="148">app.js</text>
  </g>
  <g v-click="2">
    <path d="M244 96 H342 m-10 -7 10 7 -10 7" fill="none" stroke="#67e8f9" stroke-width="2" />
    <text x="293" y="77" text-anchor="middle" fill="#67e8f9" style="font-size: 22px">Upload</text>
    <rect x="358" y="43" width="186" height="108" rx="12" fill="#132a32" stroke="#67e8f9" stroke-width="2" />
    <image href="/zurich-cloud.svg" x="371" y="55" width="160" height="24">
      <title>ZurichCloud</title>
    </image>
    <text x="451" y="121" text-anchor="middle" fill="#67e8f9" style="font-size: 30px">CDN</text>
  </g>
  <g v-click="3">
    <path d="M562 96 H660 m-10 -7 10 7 -10 7" fill="none" stroke="#67e8f9" stroke-width="2" />
    <text x="611" y="77" text-anchor="middle" fill="#67e8f9" style="font-size: 22px">Serve</text>
    <rect x="676" y="43" width="182" height="108" rx="12" fill="#17202e" stroke="#94a3b8" stroke-width="2" />
    <path d="M676 66 H858" stroke="#94a3b8" stroke-width="2" />
    <circle cx="692" cy="55" r="3" fill="#94a3b8" />
    <circle cx="705" cy="55" r="3" fill="#94a3b8" />
    <circle cx="718" cy="55" r="3" fill="#94a3b8" />
    <image href="/patak-cat.png" x="728" y="70" width="78" height="78">
      <title>patak's cat</title>
    </image>
  </g>
</svg>

<div class="leading-9">Users bring a git repo.</div>

<div v-click="1" class="leading-9">The repo contains static files: HTML, CSS, JS.</div>

<div v-click="2" class="leading-9">ZurichCloud uploads them to its CDN<span v-click="3"> and serves them.</span></div>

<Achievement v-click="4">Congratulations, you've built a clone of GitHub Pages, c. 2008!</Achievement>

<style>
h1 { margin-bottom: 12px !important; }
h2 { margin-bottom: 12px !important; }
</style>

<!--
[Section 1: about 3 minutes total.]

Okay, so what does it take to deploy a website?

Let's start with the simplest possible thing. You've got some HTML, some CSS, maybe a bit of JavaScript. There's no framework. There's nothing to build. You already have the website.

What do we actually need to know to deploy it?
-->

---
level: 2
class: authored site-directory-demo
---

# Better DX: serve a directory

<LevelBadge :number="2">Static++</LevelBadge>

<div class="two-up">
<div>

<pre class="slidev-code"><code><span :class="{ 'opacity-30': $clicks >= 1 }">bin/
  slop.go</span>
<span class="text-amber-300">site/</span>
  <span :class="{ 'text-fuchsia-300': $clicks >= 3 }">about.html</span>
  favicon.ico
  index.html
  js/
    oops-crypto-miner.js
  styles.css
<span :class="{ 'opacity-30': $clicks >= 1 }">README.md</span></code></pre>

</div>
<div>

<div v-click="1" class="big-line">The user tells us to serve just <code class="text-amber-300">site/</code>:</div>

<CodeBlockWrapper v-click="2" title="zurich.json">
<pre class="slidev-code"><code>{
  "name": "hello",
  "publish_dir": "<span class="text-amber-300">site/</span>"
}</code></pre>
</CodeBlockWrapper>

</div>

</div>

<div v-click="3">

<div class="mb-2"><code class="text-amber-300">site/</code> becomes the base:</div>

<pre class="slidev-code"><code>https://hello.zurich.cloud/<span class="text-fuchsia-300">about</span></code></pre>

</div>

<style>
h1 { margin-bottom: 12px !important; }
</style>

<!--
We need to know which directory contains the stuff you want to deploy. Here it's `site/`.

We upload those files to be served when someone requests them. There's no server application to start. The files are the thing we're deploying. The platform needs their location; it doesn't need to know how we wrote them.

Source: https://docs.netlify.com/build/configure-builds/file-based-configuration/
-->

---
level: 2
class: authored
---

# ZurichCloud's top user requests...

<LevelBadge :number="2">Static++</LevelBadge>

<div class="grid grid-cols-[280px_1fr] gap-7" style="--slidev-code-line-height: 1.2">
<div>

<div v-click="1">
  <div class="request-label">Redirects:</div>
  <div class="font-mono">/old → /new</div>
  <div class="mt-2 text-slate-300">301 Moved Permanently</div>
</div>

<div v-click="4" class="mt-3">
  <div class="request-label">Rewrites:</div>
  <div class="font-mono">/* → /index.html</div>
</div>

<div v-click="6" class="mt-3">
  <div class="request-label">Response headers:</div>
  <div class="font-mono text-[18px]">X-Content-Type-Options:<br>nosniff</div>
</div>

</div>
<div v-click="2">

````md magic-move [zurich.json] {at:3, duration:700}
```json {1,4}
{
  "name": "hello",
  "publish_dir": "site/"
}
```

```json {1,4-7|1,4-7}
{
  "name": "hello",
  "publish_dir": "site/",
  "redirects": {
    "/old": { "to": "/new", "status": 301 }
  }
}
```

```json {1,4-8|1,4-8}
{
  "name": "hello",
  "publish_dir": "site/",
  "redirects": {
    "/old": { "to": "/new", "status": 301 }
  },
  "rewrites": { "/*": "/index.html" }
}
```

```json {1,4-11|1,4-11}
{
  "name": "hello",
  "publish_dir": "site/",
  "redirects": {
    "/old": { "to": "/new", "status": 301 }
  },
  "rewrites": { "/*": "/index.html" },
  "headers": {
    "/*": { "X-Content-Type-Options": "nosniff" }
  }
}
```
````

</div>
</div>

<Achievement v-click="8">Congratulations, you've built a clone of Netlify's predecessor BitBalloon, c. 2013!</Achievement>

<style>
h1 { margin-bottom: 8px !important; }
h2 { margin-bottom: 8px !important; }
.request-label {
  margin-bottom: 8px;
  font-weight: 600;
  text-decoration: underline;
  text-decoration-color: #94a3b8;
  text-decoration-thickness: 1px;
  text-underline-offset: 6px;
}
</style>

<!--
You can also configure redirects and static response headers. Maybe this old URL should redirect to that new URL. Maybe you want a header on your static files.

Click 1 shows the redirect request. Click 2 brings back the existing config; click 3 adds the redirect with an explicit 301 status. Click 4 introduces the SPA rewrite, and click 5 adds it. Click 6 introduces the header request, and click 7 adds its configuration. Click 8 reveals the congratulations. The name and publish directory stay faded throughout.

For an SPA, unmatched paths should serve index.html without changing the browser's URL. In our made-up platform, existing static files take priority over this fallback rewrite.

So we add three fields to our made-up zurich.json: redirects maps an old path to a destination and status, rewrites maps a request path to the file to serve, and headers assigns response headers to matching paths.

This is our invented configuration format for ZurichCloud. Other platforms express these rules differently.

We don't need to write a backend for either of these things. We'll come back to them, because frameworks sometimes have their own way of expressing the same configuration.

These header rules apply to static responses. A function sets its own response headers.
-->
