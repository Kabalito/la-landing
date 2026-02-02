<script setup lang="ts">
import { useMouse } from '@vueuse/core'
import { useGenerateImageVariant } from '@/@core/composable/useGenerateImageVariant'
import heroDashboardImgDark from '@images/front-pages/landing-page/hero-dashboard-dark.png'
import heroDashboardImgLight from '@images/front-pages/landing-page/hero-dashboard-light.png'

import heroElementsImgDark from '@images/front-pages/landing-page/hero-elements-dark.png'
import heroElementsImgLight from '@images/front-pages/landing-page/hero-elements-light.png'

import volkswagen from '@images/cars/volkswagen.png'

const heroElementsImg = useGenerateImageVariant(heroElementsImgLight, heroElementsImgDark)
const heroDashboardImg = useGenerateImageVariant(heroDashboardImgLight, heroDashboardImgDark)

const { x, y } = useMouse({ touch: false })

const translateMouse = computed(() => {
  if (typeof window !== 'undefined') {
    const rotateX = ref((window.innerHeight - (1 * y.value)) / 100)

    return { transform: `perspective(1200px) rotateX(${rotateX.value < -40 ? -20 : rotateX.value}deg) rotateY(${(window.innerWidth - (2 * x.value)) / 100}deg) scale3d(1,1,1)` }
  }

  // Provide a default return value when `window` is undefined
  return { transform: 'perspective(1200px) rotateX(0deg) rotateY(0deg) scale3d(1,1,1)' }
})
</script>

<template>
  <div
    id="home"
    :style="{ background: 'rgb(var(--v-theme-surface))' }"
  >
    <div id="landingHero">
      <section class="landing-hero d-flex align-center">
        <VContainer>
          <VRow class="align-center">
            <VCol
              cols="12"
              md="6"
            >
              <div class="hero-text-box">
                <h1 class="hero-title mb-4">
                  Planifica tu viaje con GoDrive
                </h1>
                <p class="text-body-1 mb-6">
                  Olvídate del papeleo eterno. Renta fácil, maneja seguro y llega más lejos.
                </p>

                <VCard
                  class="pa-4 mb-6"
                  :style="{ borderRadius: '12px' }"
                >
                  <div class="text-subtitle-1 mb-4">
                    ¿A dónde vamos hoy?
                  </div>
                  <VRow>
                    <VCol
                      cols="12"
                      sm="6"
                    >
                      <VTextField
                        label="Recogida"
                        placeholder="Ciudad u oficina"
                        prepend-inner-icon="tabler-map-pin"
                        hide-details="auto"
                      />
                    </VCol>
                    <VCol
                      cols="12"
                      sm="6"
                    >
                      <VTextField
                        label="Entrega"
                        placeholder="Ciudad u oficina"
                        prepend-inner-icon="tabler-flag"
                        hide-details="auto"
                      />
                    </VCol>
                    <VCol
                      cols="12"
                      sm="6"
                    >
                      <VTextField
                        type="date"
                        label="Fecha de recogida"
                        prepend-inner-icon="tabler-calendar"
                        hide-details="auto"
                      />
                    </VCol>
                    <VCol
                      cols="12"
                      sm="6"
                    >
                      <VTextField
                        type="date"
                        label="Fecha de entrega"
                        prepend-inner-icon="tabler-calendar-event"
                        hide-details="auto"
                      />
                    </VCol>
                    <VCol cols="12">
                      <VBtn
                        color="primary"
                        class="w-100"
                        size="large"
                      >
                        ¡LET'S GO! Buscar Auto
                      </VBtn>
                    </VCol>
                  </VRow>
                </VCard>
              </div>
            </VCol>
            <VCol
              cols="12"
              md="6"
              class="position-relative"
            >
              <div class="hero-animation-img">
                <VImg
                  :src="volkswagen"
                  class="hero-dashboard-img"
                />
                <VImg
                  :src="heroElementsImg"
                  class="hero-elements-img"
                  :style="translateMouse"
                />
              </div>
            </VCol>
          </VRow>
        </VContainer>
      </section>

      <!--
        <VContainer>
        <div class="position-relative">
        <div class="blank-section" />
        <div class="hero-animation-img position-absolute">
        <NuxtLink
        :to="{ path: '/' }"
        target="_blank"
        >
        <div
        class="hero-dashboard-img position-relative"
        :style="translateMouse"
        data-allow-mismatch
        >
        <img
        :src="heroDashboardImg"
        alt="Hero Dashboard"
        class="animation-img"
        >
        <img
        :src="heroElementsImg"
        alt="hero elements"
        class="hero-elements-img animation-img position-absolute"
        style="transform: translateZ(1rem);"
        >
        </div>
        </NuxtLink>
        </div>
        </div>
        </VContainer>
      -->
    </div>
  </div>
</template>

<style lang="scss" scoped>
.landing-hero {
  border-radius: 0 0 50px 50px;
  padding-block: 9.75rem 22rem;
}

.hero-animation-img {
  inline-size: 90%;
  inset-block-start: -25rem;
  inset-inline-start: 4.425rem;
  margin-inline: auto;
}

section {
  display: block;
}

.blank-section {
  background-color: rgba(var(--v-theme-surface));
  min-block-size: 25rem;
}

@media (min-width: 1280px) and (max-width: 1440px) {
  .blank-section {
    min-block-size: 18rem;
  }

  .landing-hero {
    padding-block-end: 22rem;
  }

  .hero-animation-img {
    inset-block-start: -25rem;
  }
}

@media (min-width: 900px) and (max-width: 1279px) {
  .blank-section {
    min-block-size: 13rem;
  }

  .landing-hero {
    padding-block-end: 14rem;
  }

  .hero-animation-img {
    inset-block-start: -17rem;
    inset-inline-start: 2.75rem;
  }
}

@media (min-width: 768px) and (max-width: 899px) {
  .blank-section {
    min-block-size: 12rem;
  }

  .landing-hero {
    padding-block-end: 12rem;
  }

  .hero-animation-img {
    inset-block-start: -15rem;
    inset-inline-start: 2.5rem;
  }
}

@media (min-width: 600px) and (max-width: 767px) {
  .blank-section {
    min-block-size: 12rem;
  }

  .landing-hero {
    padding-block-end: 8rem;
  }

  .hero-animation-img {
    inset-block-start: -11rem;
    inset-inline-start: 2rem;
  }
}

@media (min-width: 425px) and (max-width: 600px) {
  .blank-section {
    min-block-size: 8rem;
  }

  .landing-hero {
    padding-block-end: 8rem;
  }

  .hero-animation-img {
    inset-block-start: -9rem;
    inset-inline-start: 1.7rem;
  }
}

@media (min-width: 300px) and (max-width: 424px) {
  .blank-section {
    min-block-size: 4rem;
  }

  .landing-hero {
    padding-block-end: 6rem;
  }

  .hero-animation-img {
    inset-block-start: -7rem;
    inset-inline-start: 1.25rem;
  }
}

.landing-hero::before {
  position: absolute;
  background-repeat: no-repeat;
  inset-block: 0;
  opacity: 0.5;
}

.landing-hero-dark-bg {
  background-color: #25293c;
  background-image: url("@images/front-pages/backgrounds/hero-bg.png");
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}

.landing-hero-light-bg {
  background: url("@images/front-pages/backgrounds/hero-bg.png") center no-repeat, linear-gradient(138.18deg, #eae8fd 0%, #fce5e6 94.44%);
  background-size: cover;
}

@media (min-width: 650px) {
  .hero-text-box {
    inline-size: 38rem;
    margin-block-end: 1rem;
    margin-inline: auto;
  }
}

@media (max-width: 599px) {
  .hero-title {
    font-size: 1.5rem !important;
    line-height: 2.375rem !important;
  }
}

.hero-title {
  animation: shine 2s ease-in-out infinite alternate;
  background: linear-gradient(135deg, #28c76f 0%, #5a4aff 47.92%, #ff3739 100%);
  //  stylelint-disable-next-line property-no-vendor-prefix
  -webkit-background-clip: text;
  background-clip: text;
  background-size: 200% auto;
  font-size: 42px;
  font-weight: 800;
  line-height: 48px;
  -webkit-text-fill-color: rgba(0, 0, 0, 0%);
}

@keyframes shine {
  0% {
    background-position: 0% 50%;
  }

  80% {
    background-position: 50% 90%;
  }

  100% {
    background-position: 91% 100%;
  }
}

.hero-dashboard-img {
  margin-block: 0;
  margin-inline: auto;
  transform-style: preserve-3d;
  transition: all 0.35s;

  img {
    inline-size: 100%;
  }
}

.hero-elements-img {
  position: absolute;
  inset-block: 0;
  inset-inline-start: 0;
}

.feature-cards {
  margin-block-start: 6.25rem;
}

.hero-btn-item {
  inset-block-start: 80%;
  inset-inline-start: 5%;
}
</style>
