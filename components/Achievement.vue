<template>
  <div class="achievement">
    <svg viewBox="0 0 32 32" class="trophy" aria-hidden="true">
      <path
        d="M10 4h12v9a6 6 0 0 1-12 0V4Zm0 3H5v4a6 6 0 0 0 6 6M22 7h5v4a6 6 0 0 1-6 6M16 19v7m-6 2h12"
        fill="none"
        stroke="currentColor"
        stroke-width="2"
        stroke-linecap="round"
        stroke-linejoin="round"
      />
    </svg>
    <div><slot /></div>
  </div>
</template>

<style scoped>
.achievement {
  display: grid;
  grid-template-columns: 32px 1fr;
  align-items: center;
  gap: 14px;
  margin-top: 12px;
  padding: 8px 14px;
  border-left: 3px solid #bef264;
  background: linear-gradient(100deg, #202b18, #171c14);
  color: #f7fee7;
  font-size: 22px;
  line-height: 1.25;
}

.trophy {
  width: 32px;
  height: 32px;
  color: #bef264;
}
</style>
