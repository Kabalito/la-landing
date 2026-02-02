<script setup lang="ts">
import { useMouse } from '@vueuse/core'
import { useDisplay } from 'vuetify'

const display = useDisplay()
const mode = ref<'developer' | 'designer'>('developer')
const { x, y } = useMouse({ touch: false })

const translateMouse = computed(() => {
  if (typeof window !== 'undefined' && display.mdAndUp.value) {
    const rotateX = ref((window.innerHeight - (1 * y.value)) / 120)

    return {
      transform: `perspective(1200px)
                  rotateX(${rotateX.value < -20 ? -10 : rotateX.value * 0.4}deg)
                  rotateY(${(window.innerWidth - (2 * x.value)) / 120}deg)
                  scale3d(1.03, 1.03, 1.03)`,
    }
  }

  return { transform: 'perspective(1200px) rotateX(0deg) rotateY(0deg) scale3d(1,1,1)' }
})
</script>

<template>
  <div
    id="home"
    class="hero-section"
  >
    <div id="landingHero">
      <div
        class="hero-wrapper"
        :class="mode === 'developer' ? 'mode-developer' : 'mode-designer'"
      >
        <VContainer class="hero-container">
          <VRow class="align-center justify-space-between">
            <VCol
              cols="12"
              md="6"
              lg="6"
              order-md="1"
              order="2"
            >
              <div class="hero-text text-center text-md-start">
                <VChip
                  label
                  color="primary"
                  size="small"
                  class="mb-4"
                >
                  Portafolio Profesional
                </VChip>

                <h1 class="hero-title mb-4">
                  Donde la Lógica del Código se encuentra con la Creatividad del Diseño.
                </h1>
                <p class="hero-subtitle text-body-1 mb-6">
                  Desarrollador Frontend Vue.js & Diseñador UI con más de 7 años creando experiencias digitales que funcionan y venden.
                </p>

                <div class="hero-cta d-flex flex-column flex-sm-row align-center justify-center justify-md-start gap-4">
                  <VBtn
                    color="primary"
                    :size="display.smAndUp ? 'large' : 'default'"
                    :to="{ path: '/', hash: '#portfolio' }"
                    class="font-weight-bold"
                  >
                    Ver mis Proyectos
                  </VBtn>
                  <VBtn
                    variant="outlined"
                    :size="display.smAndUp ? 'large' : 'default'"
                    :to="{ path: '/', hash: '#contact' }"
                  >
                    Hablemos
                  </VBtn>
                </div>

                <div class="mode-switch mt-8">
                  <div class="text-caption text-medium-emphasis mb-2">
                    Cambia el enfoque:
                  </div>
                  <VBtnToggle
                    v-model="mode"
                    divided
                    color="primary"
                    variant="tonal"
                    class="mode-toggle"
                    mandatory
                  >
                    <VBtn value="developer">
                      <VIcon
                        icon="tabler-code"
                        class="me-2"
                      />
                      Developer
                    </VBtn>
                    <VBtn value="designer">
                      <VIcon
                        icon="tabler-palette"
                        class="me-2"
                      />
                      Designer
                    </VBtn>
                  </VBtnToggle>
                </div>
              </div>
            </VCol>

            <VCol
              cols="12"
              md="6"
              lg="5"
              order-md="2"
              order="1"
            >
              <div
                class="hero-visual"
                :style="translateMouse"
              >
                <div class="visual-card">
                  <div class="visual-header">
                    <span class="dot dot-red" />
                    <span class="dot dot-yellow" />
                    <span class="dot dot-green" />
                    <span class="visual-title">
                      {{ mode === 'developer' ? 'Vue.js • TypeScript' : 'UI Kit • Branding' }}
                    </span>
                  </div>

                  <div
                    v-if="mode === 'developer'"
                    class="code-preview"
                  >
                    <pre><code>const stack = ['Vue 3', 'Pinia', 'TypeScript']
const impact = { performance: 'A+', ux: 'Premium' }

function ship(project) {
  return build(project).deploy()
}</code></pre>
                  </div>

                  <div
                    v-else
                    class="design-preview"
                  >
                    <div class="wireframe">
                      <div class="wireframe-top" />
                      <div class="wireframe-body">
                        <div class="wireframe-left" />
                        <div class="wireframe-right" />
                      </div>
                      <div class="wireframe-bottom" />
                    </div>
                    <div class="design-tags">
                      <span>Branding</span>
                      <span>UI/UX</span>
                      <span>Prototipos</span>
                    </div>
                  </div>
                </div>
              </div>
            </VCol>
          </VRow>
        </VContainer>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.hero-section {
  background: rgb(var(--v-theme-surface));
}

.hero-wrapper {
  position: relative;
  overflow: hidden;
  border-radius: 0 0 40px 40px;
  padding-block: 3rem 4rem;

  @media (min-width: 960px) {
    padding-block: 5rem 6rem;
  }
}

.hero-wrapper::before {
  position: absolute;
  background: radial-gradient(circle at 10% 10%, rgba(var(--v-theme-primary), 20%), transparent 55%);
  block-size: 100%;
  content: "";
  inline-size: 100%;
  inset: 0;
}

.mode-developer::after,
.mode-designer::after {
  position: absolute;
  background: linear-gradient(120deg, rgba(var(--v-theme-primary), 18%) 0%, rgba(var(--v-theme-primary), 2%) 55%, rgba(var(--v-theme-background), 0%) 100%);
  block-size: 100%;
  content: "";
  inline-size: 100%;
  inset: 0;
  opacity: 0.6;
}

.mode-designer::after {
  background: linear-gradient(120deg, rgba(255, 99, 132, 18%) 0%, rgba(80, 60, 220, 5%) 55%, rgba(var(--v-theme-background), 0%) 100%);
}

.hero-container {
  position: relative;
  z-index: 2;
}

.hero-title {
  font-size: clamp(1.8rem, 3vw, 3.4rem);
  font-weight: 800;
  line-height: 1.1;
}

.hero-subtitle {
  max-inline-size: 32rem;
}

.mode-toggle {
  display: inline-flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.mode-toggle :deep(.v-btn) {
  justify-content: center;
  min-inline-size: 140px;
}

.hero-visual {
  display: flex;
  align-items: center;
  justify-content: center;
}

.visual-card {
  position: relative;
  overflow: hidden;
  border-radius: 24px;
  background: rgba(var(--v-theme-surface), 95%);
  box-shadow: 0 24px 60px rgba(0, 0, 0, 16%);
  inline-size: min(100%, 480px);
  min-block-size: 320px;
  padding-block: 1.5rem;
  padding-inline: 1.5rem;
}

.visual-header {
  display: flex;
  align-items: center;
  gap: 0.4rem;
  margin-block-end: 1rem;
}

.visual-title {
  font-size: 0.85rem;
  font-weight: 600;
  margin-inline-start: auto;
  opacity: 0.7;
}

.dot {
  border-radius: 50%;
  block-size: 10px;
  inline-size: 10px;
}

.dot-red { background: #ff5f57; }
.dot-yellow { background: #ffbd2e; }
.dot-green { background: #28c840; }

.code-preview {
  border-radius: 16px;
  background: rgba(var(--v-theme-background), 80%);
  font-size: 0.8rem;
  line-height: 1.4;
  padding-block: 1rem;
  padding-inline: 1rem;
}

.code-preview pre {
  margin: 0;
  white-space: pre-wrap;
}

.design-preview {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.wireframe {
  display: grid;
  gap: 0.75rem;
}

.wireframe-top,
.wireframe-bottom {
  border-radius: 12px;
  background: rgba(var(--v-theme-primary), 8%);
  block-size: 32px;
}

.wireframe-body {
  display: grid;
  gap: 0.75rem;
  grid-template-columns: 1fr 1.3fr;
}

.wireframe-left,
.wireframe-right {
  border-radius: 16px;
  background: rgba(var(--v-theme-primary), 12%);
  block-size: 120px;
}

.design-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.design-tags span {
  border-radius: 999px;
  background: rgba(var(--v-theme-primary), 12%);
  font-size: 0.75rem;
  font-weight: 600;
  padding-block: 0.35rem;
  padding-inline: 0.75rem;
}
</style>
