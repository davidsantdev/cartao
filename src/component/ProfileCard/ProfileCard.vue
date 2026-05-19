<template>
  <div ref="wrapRef" :class="`pc-card-wrapper ${className}`.trim()" :style="cardStyle">
    <section ref="cardRef" class="pc-card">
      <div class="pc-inside">
        <div class="pc-shine" />
        <div class="pc-glare" />
        <div class="pc-grid-overlay" />
        <div class="pc-noise" />

        <!-- Avatar area -->
        <div class="pc-avatar-zone">
          <div class="pc-avatar-ring">
            <img src="../../assets/image/issam.png" alt="">
          </div>
          <div class="pc-company-badge">
            <span class="pc-company-dot" />
            <span class="pc-company-name">Alô Pará</span>
          </div>
        </div>

        <!-- Main content -->
        <div class="pc-content pc-info-content">

          <!-- Status badge -->
          <div class="pc-top-badge">
            <span class="pc-dot" />
            <span>{{ status }}</span>
          </div>

          <!-- Identity -->
          <div class="pc-identity">
            <h3 class="pc-name">{{ name }}</h3>
            <p class="pc-role">{{ title }}</p>
            <p class="pc-slogan">"{{ slogan }}"</p>
          </div>

          <!-- Divider -->
          <div class="pc-divider" />

          <!-- Stats row -->
          <div v-if="showStats" class="pc-stats-row">
            <div v-for="stat in stats" :key="stat.label" class="pc-stat">
              <span class="pc-stat-value">{{ stat.value }}</span>
              <span class="pc-stat-label">{{ stat.label }}</span>
            </div>
          </div>

          <!-- Contact info -->
          <div v-if="showUserInfo" class="pc-contact-info">
            <a v-if="phone" :href="`tel:${phone}`" class="pc-info-row">
              <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="M22 16.9v3a2 2 0 0 1-2.2 2 19.8 19.8 0 0 1-8.6-3.1 19.5 19.5 0 0 1-6-6 19.8 19.8 0 0 1-3.1-8.7A2 2 0 0 1 4.1 2h3a2 2 0 0 1 2 1.7c.1 1 .4 2 .7 2.9a2 2 0 0 1-.5 2.1L8.1 9.9a16 16 0 0 0 6 6l1.2-1.2a2 2 0 0 1 2.1-.5c.9.3 1.9.6 2.9.7A2 2 0 0 1 22 16.9z"/></svg>
              <span>{{ phone }}</span>
            </a>
            <a v-if="email" :href="`mailto:${email}`" class="pc-info-row">
              <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><rect x="2" y="4" width="20" height="16" rx="2"/><path d="m22 7-8.97 5.7a1.94 1.94 0 0 1-2.06 0L2 7"/></svg>
              <span>{{ email }}</span>
            </a>
          </div>

          <!-- Social links -->
          <div v-if="showUserInfo" class="pc-social-row">
            <a
              v-for="link in socialLinks"
              :key="link.label"
              :href="link.href"
              class="pc-social-btn"
              :aria-label="link.label"
              target="_blank"
            >
              <svg v-if="link.icon === 'instagram'" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><rect x="2" y="2" width="20" height="20" rx="5"/><circle cx="12" cy="12" r="5"/><circle cx="17.5" cy="6.5" r="1" fill="currentColor" stroke="none"/></svg>
              <svg v-else-if="link.icon === 'youtube'" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="M22 8s-.3-1.8-1.2-2.6c-1.1-1.2-2.4-1.2-3-1.3C14.9 4 12 4 12 4s-2.9 0-5.8.2c-.6.1-1.9.1-3 1.3C2.3 6.3 2 8 2 8S1.7 10 1.7 12s.3 4 .3 4 .3 1.8 1.2 2.6c1.1 1.2 2.6 1.1 3.3 1.2C8.5 20 12 20 12 20s2.9 0 5.8-.2c.6-.1 1.9-.1 3-1.3.9-.8 1.2-2.6 1.2-2.6s.3-2 .3-4-.3-4-.3-4z"/><polygon points="10,8.5 16,12 10,15.5" fill="currentColor" stroke="none"/></svg>
              <svg v-else-if="link.icon === 'whatsapp'" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="M3 21l1.65-3.8a9 9 0 1 1 3.4 2.9L3 21"/><path d="M9 10c.5 1 1 2 2 3s2 1.5 3 2"/></svg>
              <svg v-else-if="link.icon === 'globe'" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><circle cx="12" cy="12" r="10"/><path d="M2 12h20M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"/></svg>
              <svg v-else-if="link.icon === 'linkedin'" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"/><rect x="2" y="9" width="4" height="12"/><circle cx="4" cy="4" r="2"/></svg>
              <span>{{ link.label }}</span>
            </a>
          </div>

          <!-- CTA button -->
          <div
            class="pc-contact-btn"
            @click="handleContactClick"
            type="button"
            :aria-label="`Contato ${name}`"
          >
          
           
          </div>

        </div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import Dialog from '@/components/dialog.vue';
import { computed, onMounted, onUnmounted, useTemplateRef } from 'vue';

interface SocialLink {
  label: string;
  href: string;
  icon: string;
}

interface Stat {
  value: string;
  label: string;
}

interface Props {
  iconUrl?: string;
  grainUrl?: string;
  behindGradient?: string;
  innerGradient?: string;
  showBehindGradient?: boolean;
  className?: string;
  enableTilt?: boolean;
  name?: string;
  title?: string;
  slogan?: string;
  handle?: string;
  status?: string;
  contactText?: string;
  showUserInfo?: boolean;
  showStats?: boolean;
  phone?: string;
  email?: string;
  socialLinks?: SocialLink[];
  stats?: Stat[];
}

const props = withDefaults(defineProps<Props>(), {
  iconUrl: '',
  grainUrl: '',
  behindGradient: undefined,
  innerGradient: undefined,
  showBehindGradient: true,
  className: '',
  enableTilt: true,
  name: 'Issam Abou Fard',
  title: 'Fundador & CEO',
  slogan: '',
  handle: 'Alô Pará',
  status: 'Disponível para contato',
  contactText: 'Fale com o nossos colaboradores',
  showUserInfo: true,
  showStats: true,
  phone: '+55 (94) 9173-7636',
  email: 'mercadoalopara@gmail.com',
  socialLinks: () => [
    { label: 'Instagram', href: 'https://instagram.com/supermercadoalopara',   icon: 'instagram' },
    { label: 'YouTube',   href: 'https://youtube.com/@supermercadoalopara5866',    icon: 'youtube'   },
    { label: 'LinkedIn',  href: 'https://www.linkedin.com/in/supermercado-al%C3%B4-par%C3%A1-514228156/', icon: 'linkedin'  },
    { label: 'WhatsApp',  href: 'https://wa.me/559491737636',      icon: 'whatsapp'  },
  
  ],
  stats: () => [
    { value: '20+',   label: 'Anos de Empresa' },
    { value: '16,2K', label: 'Seguidores' },
    { value: '50K+',  label: 'Clientes atendidos' },
  ],
});

const emit = defineEmits<{ contactClick: [] }>();

const wrapRef = useTemplateRef<HTMLDivElement>('wrapRef');
const cardRef = useTemplateRef<HTMLElement>('cardRef');

const initials = computed(() => {
  return props.name
    .split(' ')
    .slice(0, 2)
    .map(w => w[0])
    .join('')
    .toUpperCase();
});

const DEFAULT_BEHIND_GRADIENT = `
  radial-gradient(farthest-side circle at var(--pointer-x) var(--pointer-y),
    hsla(0, 90%, 40%, var(--card-opacity)) 0%,
    hsla(0, 80%, 30%, calc(var(--card-opacity)*0.4)) 35%,
    transparent 72%
  ),
  radial-gradient(55% 70% at 50% 0%, #aa000040 0%, transparent 100%),
  radial-gradient(100% 100% at 50% 50%, #88000022 0%, transparent 80%)
`;

const DEFAULT_INNER_GRADIENT = 'linear-gradient(170deg, rgba(200,20,20,0.04) 0%, rgba(0,0,0,0) 55%)';

const ANIMATION_CONFIG = {
  SMOOTH_DURATION: 700,
  INITIAL_DURATION: 1500,
  INITIAL_X_OFFSET: 70,
  INITIAL_Y_OFFSET: 60,
} as const;

const clamp = (v: number, min = 0, max = 100) => Math.min(Math.max(v, min), max);
const round = (v: number, p = 3) => parseFloat(v.toFixed(p));
const adjust = (v: number, fMin: number, fMax: number, tMin: number, tMax: number) =>
  round(tMin + ((tMax - tMin) * (v - fMin)) / (fMax - fMin));
const easeInOutCubic = (x: number) => (x < 0.5 ? 4 * x * x * x : 1 - Math.pow(-2 * x + 2, 3) / 2);

let rafId: number | null = null;

const updateCardTransform = (offsetX: number, offsetY: number, card: HTMLElement, wrap: HTMLElement) => {
  const w = card.clientWidth;
  const h = card.clientHeight;
  const px = clamp((100 / w) * offsetX);
  const py = clamp((100 / h) * offsetY);
  const cx = px - 50;
  const cy = py - 50;

  const cssProps: Record<string, string> = {
    '--pointer-x': `${px}%`,
    '--pointer-y': `${py}%`,
    '--background-x': `${adjust(px, 0, 100, 35, 65)}%`,
    '--background-y': `${adjust(py, 0, 100, 35, 65)}%`,
    '--pointer-from-center': `${clamp(Math.hypot(py - 50, px - 50) / 50, 0, 1)}`,
    '--pointer-from-top': `${py / 100}`,
    '--pointer-from-left': `${px / 100}`,
    '--rotate-x': `${round(-(cx / 5))}deg`,
    '--rotate-y': `${round(cy / 4)}deg`,
  };
  Object.entries(cssProps).forEach(([k, v]) => wrap.style.setProperty(k, v));
};

const createSmoothAnimation = (duration: number, startX: number, startY: number, card: HTMLElement, wrap: HTMLElement) => {
  const startTime = performance.now();
  const targetX = wrap.clientWidth / 2;
  const targetY = wrap.clientHeight / 2;
  const loop = (now: number) => {
    const elapsed = now - startTime;
    const progress = clamp(elapsed / duration);
    const eased = easeInOutCubic(progress);
    updateCardTransform(adjust(eased, 0, 1, startX, targetX), adjust(eased, 0, 1, startY, targetY), card, wrap);
    if (progress < 1) rafId = requestAnimationFrame(loop);
  };
  rafId = requestAnimationFrame(loop);
};

const cancelAnimation = () => { if (rafId) { cancelAnimationFrame(rafId); rafId = null; } };

const handlePointerMove = (e: PointerEvent) => {
  const card = cardRef.value; const wrap = wrapRef.value;
  if (!card || !wrap || !props.enableTilt) return;
  const rect = card.getBoundingClientRect();
  updateCardTransform(e.clientX - rect.left, e.clientY - rect.top, card, wrap);
};
const handlePointerEnter = () => {
  const card = cardRef.value; const wrap = wrapRef.value;
  if (!card || !wrap || !props.enableTilt) return;
  cancelAnimation(); wrap.classList.add('active'); card.classList.add('active');
};
const handlePointerLeave = (e: PointerEvent) => {
  const card = cardRef.value; const wrap = wrapRef.value;
  if (!card || !wrap || !props.enableTilt) return;
  createSmoothAnimation(ANIMATION_CONFIG.SMOOTH_DURATION, e.offsetX, e.offsetY, card, wrap);
  wrap.classList.remove('active'); card.classList.remove('active');
};

/* ── Giroscópio (mobile) ── */
let orientationHandler: ((e: DeviceOrientationEvent) => void) | null = null;

const cardStyle = computed(() => ({
  '--icon': props.iconUrl ? `url(${props.iconUrl})` : 'none',
  '--grain': props.grainUrl ? `url(${props.grainUrl})` : 'none',
  '--behind-gradient': props.showBehindGradient ? (props.behindGradient ?? DEFAULT_BEHIND_GRADIENT) : 'none',
  '--inner-gradient': props.innerGradient ?? DEFAULT_INNER_GRADIENT,
}));

const handleContactClick = () => emit('contactClick');

onMounted(() => {
  if (!props.enableTilt) return;
  const card = cardRef.value; const wrap = wrapRef.value;
  if (!card || !wrap) return;

  card.addEventListener('pointerenter', handlePointerEnter);
  card.addEventListener('pointermove', handlePointerMove);
  card.addEventListener('pointerleave', handlePointerLeave);

  const ix = wrap.clientWidth - ANIMATION_CONFIG.INITIAL_X_OFFSET;
  const iy = ANIMATION_CONFIG.INITIAL_Y_OFFSET;
  updateCardTransform(ix, iy, card, wrap);
  createSmoothAnimation(ANIMATION_CONFIG.INITIAL_DURATION, ix, iy, card, wrap);

  /* Giroscópio */
  const registerOrientation = () => {
    orientationHandler = (e: DeviceOrientationEvent) => {
      if (!card || !wrap) return;
      const beta  = Math.max(-30, Math.min(30, e.beta  ?? 0));
      const gamma = Math.max(-30, Math.min(30, e.gamma ?? 0));
      const px = ((gamma + 30) / 60) * card.clientWidth;
      const py = ((beta  + 30) / 60) * card.clientHeight;
      cancelAnimation();
      updateCardTransform(px, py, card, wrap);
      wrap.classList.add('active');
      card.classList.add('active');
    };
    window.addEventListener('deviceorientation', orientationHandler);
  };

  if (typeof window !== 'undefined' && 'DeviceOrientationEvent' in window) {
    const DOE = DeviceOrientationEvent as any;
    if (typeof DOE.requestPermission === 'function') {
      /* iOS 13+ — requer gesto do usuário; acionado no botão CTA */
      (window as any).__requestGyro = async () => {
        try {
          const res = await DOE.requestPermission();
          if (res === 'granted') registerOrientation();
        } catch {}
      };
    } else {
      registerOrientation();
    }
  }
});

onUnmounted(() => {
  const card = cardRef.value;
  if (card) {
    card.removeEventListener('pointerenter', handlePointerEnter);
    card.removeEventListener('pointermove', handlePointerMove);
    card.removeEventListener('pointerleave', handlePointerLeave);
  }
  if (orientationHandler) window.removeEventListener('deviceorientation', orientationHandler);
  cancelAnimation();
});
</script>

<style scoped>
/* ── Variáveis & wrapper ── */
.pc-card-wrapper {
  --pointer-x: 50%;
  --pointer-y: 50%;
  --pointer-from-center: 0;
  --pointer-from-top: 0.5;
  --pointer-from-left: 0.5;
  --card-opacity: 0;
  --rotate-x: 0deg;
  --rotate-y: 0deg;
  --background-x: 50%;
  --background-y: 50%;
  --grain: none;
  --icon: none;
  --behind-gradient: none;
  --inner-gradient: none;

  --neon: #cc1a1a;
  --neon-dim: rgba(180, 20, 20, 0.12);
  --neon-glow: rgba(180, 20, 20, 0.35);
  --card-radius: 22px;

  perspective: 700px;
  transform: translate3d(0, 0, 0.1px);
  position: relative;
  touch-action: none;
  width: fit-content;
}

.pc-card-wrapper::before {
  content: '';
  position: absolute;
  inset: -14px;
  border-radius: inherit;
  background-image: var(--behind-gradient);
  background-size: 100% 100%;
  filter: blur(42px) opacity(0);
  transform: scale(0.86) translate3d(0, 0, 0.1px);
  transition: filter 0.5s ease, transform 0.5s ease;
}
.pc-card-wrapper:hover::before,
.pc-card-wrapper.active::before {
  --card-opacity: 1;
  filter: blur(42px) opacity(0.55);
  transform: scale(0.93) translate3d(0, 0, 0.1px);
}
.pc-card-wrapper:hover,
.pc-card-wrapper.active { --card-opacity: 1; }

/* ── Card shell ── */
.pc-card {
  width: 440px;
 
  aspect-ratio: 0.62;
  border-radius: var(--card-radius);
  position: relative;
  overflow: hidden;
  transition: transform 1s ease, box-shadow 0.4s ease;
  transform: translate3d(0, 0, 0.1px) rotateX(0deg) rotateY(0deg);
  box-shadow:
    0 0 0 1px rgba(255,255,255,0.06),
    0 28px 56px rgba(0,0,0,0.75);
  background: #0a0a0a;
}
.pc-card:hover,
.pc-card.active {
  transition: none;
  transform: translate3d(0, 0, 0.1px) rotateX(var(--rotate-y)) rotateY(var(--rotate-x));
  box-shadow:
    0 0 0 1px rgba(180,20,20,0.22),
    0 0 28px rgba(180,20,20,0.1),
    0 36px 72px rgba(0,0,0,0.85);
}

.pc-card * {
  border-radius: var(--card-radius);
  transform: translate3d(0, 0, 0.1px);
}

/* ── Interior ── */
.pc-inside {
  position: absolute;
  inset: 1px;
  background-image: var(--inner-gradient);
  background-color: #0a0a0a;
  border-radius: calc(var(--card-radius) - 1px);
  overflow: hidden;
}

/* ── Grid overlay ── */
.pc-grid-overlay {
  position: absolute;
  inset: 0;
  background-image: radial-gradient(circle, rgba(255,255,255,0.03) 1px, transparent 1px);
  background-size: 22px 22px;
  mix-blend-mode: screen;
  opacity: 0.5;
  pointer-events: none;
  z-index: 1;
  border-radius: 0;
}

/* ── Noise texture ── */
.pc-noise {
  position: absolute;
  inset: 0;
  opacity: 0.025;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
  background-size: 128px 128px;
  pointer-events: none;
  z-index: 2;
  border-radius: 0;
  mix-blend-mode: overlay;
}

/* ── Shine ── */
.pc-shine {
  position: absolute;
  inset: 0;
  mask-image: var(--icon);
  mask-mode: luminance;
  mask-repeat: repeat;
  mask-size: 150%;
  mask-position: top calc(200% - (var(--background-y) * 5)) left calc(100% - var(--background-x));
  -webkit-mask-image: var(--icon);
  -webkit-mask-mode: luminance;
  -webkit-mask-repeat: repeat;
  -webkit-mask-size: 150%;
  -webkit-mask-position: top calc(200% - (var(--background-y) * 5)) left calc(100% - var(--background-x));
  filter: brightness(0.4) contrast(1.1) saturate(0.15) opacity(0.3);
  mix-blend-mode: color-dodge;
  z-index: 3;
  border-radius: 0;

  --space: 14.28%;
  background-image:
    repeating-linear-gradient(
      0deg,
      hsl(0,  85%, 48%) calc(var(--space) * 1),
      hsl(10, 80%, 52%) calc(var(--space) * 2),
      hsl(350,75%, 46%) calc(var(--space) * 3),
      hsl(0,  65%, 38%) calc(var(--space) * 4),
      hsl(5,  85%, 50%) calc(var(--space) * 5),
      hsl(355,80%, 44%) calc(var(--space) * 6),
      hsl(0,  85%, 48%) calc(var(--space) * 7)
    ),
    repeating-linear-gradient(
      -45deg,
      #0a0a0a 0%,
      hsl(0, 5%, 18%) 3.8%,
      hsl(0, 7%, 22%) 4.5%,
      hsl(0, 5%, 18%) 5.2%,
      #0a0a0a 10%,
      #0a0a0a 12%
    ),
    radial-gradient(
      farthest-corner circle at var(--pointer-x) var(--pointer-y),
      hsla(0,0%,0%,0.08) 12%,
      hsla(0,0%,0%,0.12) 20%,
      hsla(0,0%,0%,0.22) 120%
    );
  background-position: 0 var(--background-y), var(--background-x) var(--background-y), center;
  background-blend-mode: color, hard-light;
  background-size: 500% 500%, 300% 300%, 200% 200%;
}
.pc-card:hover .pc-shine,
.pc-card.active .pc-shine {
  filter: brightness(0.55) contrast(1.2) saturate(0.25) opacity(0.55);
}

/* ── Glare — suave ── */
.pc-glare {
  position: absolute;
  inset: 0;
  border-radius: 0;
  background-image: radial-gradient(
    farthest-corner circle at var(--pointer-x) var(--pointer-y),
    hsla(0, 8%, 55%, 0.06) 12%,
    hsla(0, 4%, 10%, 0.32) 90%
  );
  mix-blend-mode: soft-light;
  filter: brightness(0.85) contrast(1.0);
  z-index: 4;
}

/* ── Avatar zone ── */
.pc-avatar-zone {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 52%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 14px;
  z-index: 5;
  background: linear-gradient(
    to bottom,
    rgba(30,0,0,0.5) 0%,
    rgba(10,10,10,0.0) 70%
  );
  pointer-events: none;
  border-radius: 0;
}

.pc-avatar-ring {
  width: 208px;
  height: 208px;
  border-radius: 50% !important;
  background: linear-gradient(135deg, #2a0000, #1a0000);
  border: 1.5px solid rgba(180,20,20,0.4);
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow:
    0 0 0 4px rgba(180,20,20,0.08),
    0 0 32px rgba(180,20,20,0.2),
    inset 0 1px 0 rgba(255,100,100,0.1);
  position: relative;
}

.pc-avatar-ring::before {
  content: '';
  position: absolute;
  inset: -4px;
  border-radius: 50%;
  border: 1px solid rgba(180,20,20,0.15);
  animation: ring-pulse 3s ease-in-out infinite;
}

@keyframes ring-pulse {
  0%, 100% { transform: scale(1); opacity: 0.6; }
  50% { transform: scale(1.05); opacity: 0.2; }
}

.pc-avatar-initials {
  font-size: 28px;
  font-weight: 700;
  letter-spacing: -1px;
  background: linear-gradient(160deg, #ffffff 20%, #ff7070 100%);
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  border-radius: 0 !important;
  line-height: 1;
}

.pc-company-badge {
  display: flex;
  align-items: center;
  gap: 6px;
  background: rgba(180,20,20,0.12);
  border: 1px solid rgba(180,20,20,0.25);
  border-radius: 20px !important;
  padding: 4px 12px;
}

.pc-company-dot {
  width: 5px;
  height: 5px;
  border-radius: 50% !important;
  background: #cc1a1a;
  box-shadow: 0 0 5px #cc1a1a;
  animation: blink 2.5s ease-in-out infinite;
  flex-shrink: 0;
}

.pc-company-name {
  font-size: 10px;
  font-weight: 600;
  color: #ff6666;
  letter-spacing: 1.2px;
  text-transform: uppercase;
  border-radius: 0 !important;
}

/* ── Content ── */
.pc-content {
  position: absolute;
  inset: 0;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  padding: 16px;
  z-index: 6;
  transform: translate3d(
    calc(var(--pointer-from-left) * -4px + 2px),
    calc(var(--pointer-from-top) * -4px + 2px),
    0.1px
  ) !important;
  border-radius: 0 !important;
  background: linear-gradient(
    to top,
    rgba(0,0,0,0.92) 0%,
    rgba(0,0,0,0.7) 40%,
    rgba(0,0,0,0.2) 70%,
    transparent 100%
  );
}

/* ── Status badge ── */
.pc-top-badge {
  position: absolute !important;
  top: 14px;
  left: 50%;
  transform: translateX(-50%) translate3d(0,0,0.1px) !important;
  display: flex !important;
  align-items: center;
  gap: 6px;
  background: rgba(180,20,20,0.1);
  border: 1px solid rgba(180,20,20,0.22);
  border-radius: 20px !important;
  padding: 3px 11px;
  white-space: nowrap;
  pointer-events: none;
}

.pc-dot {
  width: 5px;
  height: 5px;
  border-radius: 50% !important;
  background: #cc1a1a;
  box-shadow: 0 0 5px #cc1a1a;
  animation: blink 2s ease-in-out infinite;
  flex-shrink: 0;
}

@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.25; }
}

.pc-top-badge span:last-child {
  font-size: 10px;
  font-weight: 500;
  color: #ff5555;
  letter-spacing: 0.3px;
}

/* ── Identity ── */
.pc-identity {
  margin-bottom: 10px;
  text-align: center;
}

.pc-name {
  font-size: clamp(1.35rem, 5svh, 1.85rem);
  font-weight: 700;
  margin: 0 0 2px;
  letter-spacing: -0.5px;
  background: linear-gradient(160deg, #ffffff 25%, #ff8080 100%);
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  line-height: 1.1;
  border-radius: 0 !important;
}

.pc-role {
  font-size: 11px;
  font-weight: 500;
  color: rgba(255,255,255,0.4);
  letter-spacing: 1px;
  text-transform: uppercase;
  margin: 0 0 6px;
  border-radius: 0 !important;
}

.pc-slogan {
  font-size: 11.5px;
  color: rgba(255,180,180,0.5);
  font-style: italic;
  letter-spacing: 0.2px;
  margin: 0;
  border-radius: 0 !important;
}

/* ── Divider ── */
.pc-divider {
  height: 1px;
  background: linear-gradient(to right, transparent, rgba(180,20,20,0.35), transparent);
  margin: 10px 0;
  border-radius: 0 !important;
}

/* ── Stats ── */
.pc-stats-row {
  display: flex;
  justify-content: space-around;
  margin-bottom: 10px;
  border-radius: 0 !important;
}

.pc-stat {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1px;
  border-radius: 0 !important;
}

.pc-stat-value {
  font-size: 15px;
  font-weight: 700;
  color: #ff7070;
  letter-spacing: -0.3px;
  border-radius: 0 !important;
}

.pc-stat-label {
  font-size: 9.5px;
  font-weight: 500;
  color: rgba(255,255,255,0.3);
  text-transform: uppercase;
  letter-spacing: 0.8px;
  border-radius: 0 !important;
}

/* ── Contact info ── */
.pc-contact-info {
  display: flex;
  flex-direction: column;
  gap: 4px;
  margin-bottom: 8px;
  border-radius: 0 !important;
}

.pc-info-row {
  display: flex;
  align-items: center;
  gap: 7px;
  font-size: 15px;
  color: rgba(255,255,255,0.4);
  text-decoration: none;
  padding: 3px 0;
  pointer-events: auto;
  transition: color 0.2s;
  border-radius: 0 !important;
}

.pc-info-row:hover { color: rgba(255,150,150,0.75); }

.pc-info-row svg {
  flex-shrink: 0;
  border-radius: 0 !important;
  opacity: 0.6;
}

/* ── Social buttons ── */
.pc-social-row {
  display: flex;
  gap: 5px;
  justify-content: center;
  flex-wrap: wrap;
  margin-bottom: 8px;
  pointer-events: auto;
  border-radius: 0 !important;
}

.pc-social-btn {
  display: inline-flex !important;
  align-items: center;
  gap: 4px;
  background: rgba(255,255,255,0.04);
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: 7px !important;
  padding: 4px 9px;
  font-size: 10.5px;
  font-weight: 500;
  color: rgba(255,255,255,0.5);
  text-decoration: none;
  cursor: pointer;
  transition: all 0.2s ease;
  pointer-events: auto;
  letter-spacing: 0.1px;
}

.pc-social-btn svg {
  flex-shrink: 0;
  border-radius: 0 !important;
}

.pc-social-btn:hover {
  background: rgba(180,20,20,0.12);
  border-color: rgba(180,20,20,0.3);
  color: #ff8080;
}

/* ── CTA button ── */
.pc-contact-btn {
  display: flex !important;
  align-items: center;
  justify-content: center;
  gap: 7px;
  width: 100%;
  background: linear-gradient(135deg, #c01515 0%, #8a0a0a 100%);
  border: none;
  border-radius: 10px !important;
  padding: 10px;
  font-size: 12.5px;
  font-weight: 600;
  color: #fff;
  cursor: pointer;
  transition: all 0.2s ease;
  pointer-events: auto;
  letter-spacing: 0.3px;
  box-shadow:
    0 4px 18px rgba(180,20,20,0.3),
    inset 0 1px 0 rgba(255,255,255,0.1);
  border-top: 1px solid rgba(255,100,100,0.15) !important;
}

.pc-contact-btn svg {
  border-radius: 0 !important;
}

.pc-contact-btn:hover {
  background: linear-gradient(135deg, #d41818 0%, #a01010 100%);
  transform: translateY(-1px);
  box-shadow: 0 8px 26px rgba(180,20,20,0.45);
}

/* ── Responsive ── */
@media (max-width: 768px) {
  .pc-card-wrapper {
    width: 100%;
    display: flex;
    justify-content: center;
  }

  .pc-card {
    width: auto;
    height: 88dvh;
    aspect-ratio: 0.62;
    max-width: 96vw;
  }



  .pc-avatar-initials {
    font-size: clamp(22px, 5.5vw, 28px);
  }
}

@media (max-width: 480px) {
  .pc-card {
    height: 85dvh;
    max-width: 94vw;
  }

  .pc-content        { padding: 12px; }
  .pc-identity       { margin-bottom: 8px; }
  .pc-divider        { margin: 7px 0; }
  .pc-stats-row      { margin-bottom: 7px; }
  .pc-contact-info   { margin-bottom: 6px; }
  .pc-social-row     { margin-bottom: 6px; }
  .pc-social-btn     { font-size: 9.5px; padding: 3px 7px; }
  .pc-contact-btn    { font-size: 12px; padding: 9px; }
}
</style>