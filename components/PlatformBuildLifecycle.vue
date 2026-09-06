<template>
  <svg
    viewBox="0 0 868 116"
    role="img"
    aria-label="ZurichCloud runs the user's build command, then the build plugin's onBuild hook, then deploys the result."
  >
    <image href="/zurich-cloud.svg" x="4" y="0" width="142" height="26" />
    <text x="160" y="21" class="heading">build pipeline</text>

    <rect x="4" y="42" width="238" height="64" />
    <text x="123" y="82" text-anchor="middle" class="command">
      $ next build
    </text>
    <path d="M254 74H298m-7-6 7 6-7 6" />
    <rect x="310" y="42" width="286" height="64" />
    <text x="453" y="66" text-anchor="middle" class="heading">
      Our build plugin
    </text>
    <text x="453" y="92" text-anchor="middle" class="command">onBuild()</text>
    <path d="M608 74H652m-7-6 7 6-7 6" />
    <rect x="664" y="42" width="200" height="64" />
    <text x="764" y="82" text-anchor="middle">Deploy</text>
  </svg>
</template>

<style scoped>
rect {
  fill: #17202e;
  stroke: #64748b;
  stroke-width: 1.5;
  rx: 8px;
}
path {
  fill: none;
  stroke: #94a3b8;
  stroke-width: 1.5;
}
text {
  fill: #f8fafc;
  font-size: 24px;
}
.heading {
  fill: #cbd5e1;
  font-size: 20px;
}
.command {
  font-family: var(--slidev-code-font-family);
  font-size: 22px;
}
</style>
