<template>
  <!-- Botão que aciona o dialog -->
  <button class="sd-trigger-btn" @click="open = true" type="button">
    <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
      <path d="M3 21l1.65-3.8a9 9 0 1 1 3.4 2.9L3 21"/>
      <path d="M9 10c.5 1 1 2 2 3s2 1.5 3 2"/>
    </svg>
    Fale com nossos colaboradores
  </button>

  <!-- Backdrop -->
  <Transition name="sd-fade">
    <div v-if="open" class="sd-backdrop" @click="open = false" />
  </Transition>

  <!-- Dialog -->
  <Transition name="sd-slide">
    <div v-if="open" class="sd-dialog" role="dialog" aria-modal="true" aria-label="Fale com nossos setores">

      <!-- Header -->
      <div class="sd-header">
        <div class="sd-header-left">
          <div class="sd-header-dot" />
          <div>
            <h2 class="sd-title">Fale Conosco</h2>
            <p class="sd-subtitle">Escolha o setor e inicie a conversa</p>
          </div>
        </div>
        <button class="sd-close-btn" @click="open = false" aria-label="Fechar">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M18 6 6 18M6 6l12 12"/>
          </svg>
        </button>
      </div>

      <!-- Divider -->
      <div class="sd-divider" />

      <!-- Setores -->
      <div class="sd-list">
        <a
          v-for="setor in setores"
          :key="setor.nome"
          :href="waLink(setor)"
          target="_blank"
          rel="noopener"
          class="sd-item"
          @click="open = false"
        >
          <div class="sd-item-icon">
            <!-- Comercial -->
            <svg v-if="setor.icone === 'comercial'" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7">
              <path d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2 9m12-9l2 9M9 21h6"/>
            </svg>
            <!-- Suporte -->
            <svg v-else-if="setor.icone === 'suporte'" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7">
              <circle cx="12" cy="12" r="10"/>
              <path d="M9.09 9a3 3 0 0 1 5.83 1c0 2-3 3-3 3"/>
              <circle cx="12" cy="17" r="0.5" fill="currentColor"/>
            </svg>
            <!-- Financeiro -->
            <svg v-else-if="setor.icone === 'financeiro'" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7">
              <line x1="12" y1="1" x2="12" y2="23"/>
              <path d="M17 5H9.5a3.5 3.5 0 0 0 0 7h5a3.5 3.5 0 0 1 0 7H6"/>
            </svg>
            <!-- RH -->
            <svg v-else-if="setor.icone === 'rh'" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7">
              <path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/>
              <circle cx="9" cy="7" r="4"/>
              <path d="M23 21v-2a4 4 0 0 0-3-3.87"/>
              <path d="M16 3.13a4 4 0 0 1 0 7.75"/>
            </svg>
          </div>

          <div class="sd-item-info">
            <span class="sd-item-nome">{{ setor.nome }}</span>
            <span class="sd-item-desc">{{ setor.descricao }}</span>
          </div>

          <div class="sd-item-arrow">
            <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M5 12h14M12 5l7 7-7 7"/>
            </svg>
          </div>
        </a>
      </div>

      <!-- Footer -->
      <div class="sd-footer">
        <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8">
          <circle cx="12" cy="12" r="10"/>
          <polyline points="12 6 12 12 16 14"/>
        </svg>
        <span>Atendimento de seg. a sex., 8h às 18h</span>
      </div>

    </div>
  </Transition>
</template>

<script setup lang="ts">
import { ref } from 'vue';

interface Setor {
  nome: string;
  descricao: string;
  icone: string;
  wame: string;
  mensagem: string;
}

const open = ref(false);

const setores: Setor[] = [
  {
    nome: 'Comercial',
    descricao: 'Parcerias, anúncios e propostas',
    icone: 'comercial',
    wame: '559491503593',
    mensagem: 'Olá! Gostaria de falar com o setor Comercial da Alô Pará.',
  },
  {
    nome: 'Suporte',
    descricao: 'Dúvidas, reclamações e ajuda técnica',
    icone: 'suporte',
    wame: '559481369236',
    mensagem: 'Olá! Preciso de suporte da equipe da Alô Pará.',
  },
  {
    nome: 'Financeiro',
    descricao: 'Pagamentos, notas fiscais e cobranças',
    icone: 'financeiro',
    wame: '559492080029',
    mensagem: 'Olá! Gostaria de falar com o setor Financeiro da Alô Pará.',
  },
  {
    nome: 'RH',
    descricao: 'Vagas, currículos e colaboradores',
    icone: 'rh',
    wame: '559492268984',
    mensagem: 'Olá! Gostaria de falar com o RH da Alô Pará.',
  },
];

const waLink = (setor: Setor) =>
  `https://wa.me/${setor.wame}?text=${encodeURIComponent(setor.mensagem)}`;
</script>

<style scoped>
/* ── Dialog ── */
.sd-dialog {
  position: fixed;
  bottom: 0;
  left: 50%;
  transform: translate3d(-50%, 0, 0); /* FIX PRINCIPAL */
  width: min(420px, 100vw);
  background: #0e0e0e;
  border: 1px solid rgba(180,20,20,0.2);
  border-bottom: none;
  border-radius: 20px 20px 0 0;
  z-index: 101;
  overflow: hidden;
  box-shadow:
    0 -8px 40px rgba(0,0,0,0.6),
    0 0 0 1px rgba(255,255,255,0.04) inset;
}

/* ── Desktop ── */
@media (min-width: 480px) {
  .sd-dialog {
    bottom: auto;
    top: 50%;
    transform: translate3d(-50%, -50%, 0);
    border-radius: 20px;
    border-bottom: 1px solid rgba(180,20,20,0.2);
  }
}

/* ── Transitions ── */
.sd-fade-enter-active,
.sd-fade-leave-active {
  transition: opacity 0.25s ease;
}
.sd-fade-enter-from,
.sd-fade-leave-to {
  opacity: 0;
}

/* ANIMAÇÃO CORRIGIDA */
.sd-slide-enter-active,
.sd-slide-leave-active {
  transition: transform 0.35s cubic-bezier(0.32, 0.72, 0, 1), opacity 0.25s ease;
}

/* MOBILE: sobe de baixo */
.sd-slide-enter-from,
.sd-slide-leave-to {
  opacity: 0;
  transform: translate3d(-50%, 80px, 0);
}

/* DESKTOP: leve zoom */
@media (min-width: 480px) {
  .sd-slide-enter-from,
  .sd-slide-leave-to {
    opacity: 0;
    transform: translate3d(-50%, -40%, 0) scale(0.96);
  }
}
</style>