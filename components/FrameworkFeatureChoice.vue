<script setup lang="ts">
defineProps<{ step: number }>();

const features = [
  "Image CDN configuration",
  "Redirects and rewrites",
  "Static response headers",
];
</script>

<template>
  <div class="feature-choice" :class="{ coordinating: step >= 5 }">
    <p class="premise">
      By choosing a Vite-only architecture, framework authors constrain what they
      can offer.
    </p>

    <div class="configuration-map">
      <div class="column-heading feature-heading">
        The user wants to configure…
      </div>
      <div class="column-heading">
        <div class="logos">
          <img src="/tanstack.svg" alt="TanStack Start" />
          <img src="/solid.svg" alt="SolidStart" />
        </div>
        Framework
      </div>
      <div class="column-heading platform-heading">
        <div class="logos">
          <img src="/zurich-cloud-symbol.svg" alt="ZurichCloud" />
          <img src="/vite.svg" alt="Vite" />
        </div>
        Platform / plugin
      </div>

      <template v-for="(feature, index) in features" :key="feature">
        <div class="feature-name reveal" :class="{ shown: step >= index + 1 }">
          {{ feature }}
        </div>
        <div class="outside reveal" :class="{ shown: step >= index + 1 }">
          <span class="minus" aria-hidden="true">−</span> Out of scope
        </div>
        <div class="available reveal" :class="{ shown: step >= index + 1 }">
          <span class="check" aria-hidden="true">✓</span> Configure it here
        </div>
      </template>
    </div>

    <div class="takeaway reveal" :class="{ shown: step >= 4 }">
      No framework convenience. The user configures the platform directly.
    </div>

    <div class="skew reveal" :class="{ shown: step >= 5 }">
      <strong>But skew protection?</strong>
      <div class="coordination">
        <span>Framework</span>
        <span class="bridge" aria-hidden="true">⟷</span>
        <span>Platform</span>
      </div>
      <span class="both"
        >The user can’t configure away the need for coordination.</span
      >
    </div>
  </div>
</template>

<style scoped>
.feature-choice {
  height: 386px;
  position: relative;
  color: #f1f5f9;
}
.feature-choice .premise {
  margin: 0 0 14px;
  font-size: 25px;
  line-height: 1.3;
}
.configuration-map {
  display: grid;
  grid-template-columns: 1.32fr 0.9fr 1.08fr;
  gap: 6px 20px;
  align-items: stretch;
}
.column-heading {
  display: flex;
  align-items: center;
  gap: 9px;
  font-size: 22px;
  padding-bottom: 12px;
  border-bottom: 1px solid #64748b;
  white-space: nowrap;
}
.feature-heading {
  color: #cbd5e1;
  font-size: 20px;
}
.logos {
  display: flex;
  gap: 5px;
}
.logos img {
  width: 25px;
  height: 25px;
  object-fit: contain;
}
.feature-name,
.outside,
.available {
  min-height: 48px;
  display: flex;
  align-items: center;
  font-size: 23px;
}
.outside,
.available {
  gap: 10px;
  padding: 0 12px;
  border-radius: 6px;
  border: 1px solid #475569;
}
.outside {
  color: #a6b2c3;
  border-style: dashed;
}
.available {
  color: #e2f8ec;
  background: #163128;
  border-color: #5c9b7a;
}
.minus {
  color: #94a3b8;
}
.check {
  color: #86efac;
}
.takeaway {
  margin-top: 24px;
  font-size: 25px;
  line-height: 1.4;
}
.reveal {
  opacity: 0;
  visibility: hidden;
  transform: translateY(7px);
  transition:
    opacity 500ms,
    transform 500ms,
    visibility 500ms;
}
.reveal.shown {
  opacity: 1;
  visibility: visible;
  transform: none;
}
.configuration-map,
.premise,
.takeaway {
  transition: opacity 500ms;
}
.coordinating .configuration-map,
.coordinating .premise {
  opacity: 0.2;
}
.coordinating .takeaway {
  opacity: 0;
  visibility: hidden;
}
.skew {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  display: grid;
  grid-template-columns: auto 1fr;
  align-items: center;
  column-gap: 30px;
  row-gap: 8px;
  padding: 10px 22px;
  border: 1px solid #67e8f9;
  border-radius: 8px;
  background: #142c34;
  font-size: 25px;
}
.skew strong {
  font-weight: 500;
  color: #a5f3fc;
}
.coordination {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  gap: 18px;
}
.bridge {
  color: #67e8f9;
  font-size: 36px;
  line-height: 1;
}
.both {
  grid-column: 1 / -1;
  font-size: 24px;
}
@media (prefers-reduced-motion: reduce) {
  * {
    transition: none !important;
    transform: none !important;
  }
}
</style>
