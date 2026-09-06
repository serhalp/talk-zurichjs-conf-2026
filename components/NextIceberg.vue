<template>
  <svg viewBox="0 0 868 400" role="img" aria-labelledby="iceberg-title">
    <title id="iceberg-title">
      Next.js iceberg. We've only just begun to scratch the surface.
    </title>

    <path d="M8 130H860V394H8Z" fill="#142335" opacity="0.55" />

    <path d="M458 130 527 42 550 84 583 99 610 130Z" fill="#e2e8f0" />
    <path d="M458 130 527 42 508 130Z" fill="#94a3b8" />
    <path d="M527 42 550 84 537 109 508 130Z" fill="#f8fafc" />
    <path d="M550 84 583 99 610 130 537 109Z" fill="#cbd5e1" />

    <path
      d="M458 130 610 130 690 204 664 287 568 384 485 340 401 246 419 177Z"
      fill="#334b65"
    />
    <path d="M458 130 508 130 470 220 401 246 419 177Z" fill="#45617c" />
    <path d="M508 130 610 130 562 226 470 220Z" fill="#3c5672" />
    <path d="M610 130 690 204 562 226Z" fill="#293e57" />
    <path d="M690 204 664 287 568 384 562 226Z" fill="#22354c" />
    <path d="M401 246 470 220 485 340Z" fill="#2b405a" />
    <path d="M470 220 562 226 568 384 485 340Z" fill="#354961" />

    <path d="M8 130H860" stroke="#94a3b8" stroke-width="1.5" opacity="0.8" />
    <path
      d="M428 145H626M461 154H590"
      stroke="#64748b"
      stroke-width="1"
      opacity="0.5"
    />

    <image
      href="/nextjs.svg"
      x="485"
      y="247"
      width="40"
      height="40"
      class="logo"
    />
    <text x="540" y="279" class="name">Next.js</text>

    <text x="28" y="51" class="caption">
      <tspan x="28">We've only just begun</tspan>
      <tspan x="28" dy="32">to scratch the surface</tspan>
    </text>
    <path d="M390 60Q453 14 508 40m-13-1 13 1-7-11" class="arrow" />
  </svg>
</template>

<style scoped>
svg {
  width: 100%;
}
text {
  fill: #f8fafc;
}
.caption {
  font-size: 32px;
}
.name {
  font-size: 36px;
}
.logo {
  filter: brightness(0) invert(1);
}
.arrow {
  fill: none;
  stroke: #cbd5e1;
  stroke-width: 2;
  stroke-linecap: round;
  stroke-linejoin: round;
}
</style>
