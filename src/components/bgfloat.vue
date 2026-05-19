<script setup lang="ts">
import LightRays from '@/component/LightRays/LightRays.vue';
</script>

<template>
  <div class="bg-root">

    <!-- Base grid -->
    <div class="bg-grid" />

    <!-- Vignette corners -->
    <div class="bg-vignette" />

    <!-- Red ambient glow — top center -->
    <div class="bg-glow-top" />

    <!-- Light rays -->
    <div class="bg-rays-layer">
      <LightRays
        rays-origin="top-center"
        rays-color="#ff1a1a"
        :rays-speed="1.2"
        :light-spread="0.6"
        :ray-length="1.0"
        :follow-mouse="true"
        :mouse-influence="0.08"
        :noise-amount="0.08"
        :distortion="0.03"
        class-name="custom-rays"
      />
    </div>

    <!-- Scanline texture (optional — subtle depth) -->
    <div class="bg-scanlines" />

    <!-- Page content -->
    <div class="bg-content">
      <slot />
    </div>

  </div>
</template>

<style scoped>
.bg-root {
  position: relative;
  width: 100%;
  min-height: 100vh;
  background: #080808;
  overflow: hidden;
}

/* Dot grid — tighter, dimmer */
.bg-grid {
  position: absolute;
  inset: 0;
  background-image:
    radial-gradient(circle, rgba(255,255,255,0.04) 1px, transparent 1px);
  background-size: 32px 32px;
  pointer-events: none;
  z-index: 0;
}

/* Top center neon glow blob */
.bg-glow-top {
  position: absolute;
  top: -120px;
  left: 50%;
  transform: translateX(-50%);
  width: 700px;
  height: 400px;
  background: radial-gradient(
    ellipse at center,
    rgba(255, 30, 30, 0.18) 0%,
    rgba(180, 10, 10, 0.08) 45%,
    transparent 70%
  );
  filter: blur(20px);
  pointer-events: none;
  z-index: 1;
}

/* Subtle dark vignette on all four corners */
.bg-vignette {
  position: absolute;
  inset: 0;
  background: radial-gradient(
    ellipse at center,
    transparent 50%,
    rgba(0,0,0,0.65) 100%
  );
  pointer-events: none;
  z-index: 2;
}

/* Scanlines — very subtle */
.bg-scanlines {
  position: absolute;
  inset: 0;
  background: repeating-linear-gradient(
    to bottom,
    transparent,
    transparent 3px,
    rgba(0,0,0,0.06) 3px,
    rgba(0,0,0,0.06) 4px
  );
  pointer-events: none;
  z-index: 3;
}

/* Rays sit above grid, below content */
.bg-rays-layer {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  z-index: 4;
  pointer-events: none;
}

/* Content always on top */
.bg-content {
  position: relative;
  z-index: 5;
  width: 100%;
}
</style>