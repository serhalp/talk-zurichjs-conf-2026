<template>
  <svg
    viewBox="0 0 868 390"
    role="img"
    aria-label="Run next build, read .next, then use the ZurichCloud Next.js build plugin to prepare static assets, functions, edge functions, redirects, headers, Image CDN configuration, and blobs."
  >
    <rect x="2" y="141" width="156" height="66" />
    <text x="80" y="182" text-anchor="middle" class="command">
      $ next build
    </text>
    <path d="M158 174H186m-6-5 6 5-6 5" />
    <rect x="196" y="141" width="120" height="66" />
    <text x="256" y="182" text-anchor="middle" class="command next-label">
      .next/
    </text>
    <path d="M316 174H344m-6-5 6 5-6 5" />
    <rect x="354" y="141" width="246" height="66" />
    <image href="/zurich-cloud.svg" x="405" y="148" width="144" height="23" />
    <text x="477" y="197" text-anchor="middle">Next.js build plugin</text>
    <path d="M600 174H628M628 30V366" />
    <path
      v-for="y in [30, 78, 126, 174, 222, 270, 318, 366]"
      :key="y"
      :d="`M628 ${y}H654m-6-5 6 5-6 5`"
    />
    <text x="674" y="38" class="static">CDN (static assets)</text>
    <text x="674" y="86" class="function">Functions</text>
    <text x="674" y="134" class="function">Edge Functions</text>
    <text x="674" y="182">Redirects</text>
    <text x="674" y="230">Headers</text>
    <text x="674" y="278">Image CDN config</text>
    <text x="674" y="326">Blobs</text>
    <text x="674" y="374">...</text>
  </svg>
</template>

<style scoped>
svg {
  overflow: visible;
}
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
.command {
  font-family: var(--slidev-code-font-family);
  font-size: 20px;
}
.static {
  fill: #fcd34d;
}
.function {
  fill: #67e8f9;
}
</style>
