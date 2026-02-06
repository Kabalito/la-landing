<script setup lang="ts">
import Footer from '@/views/front-pages/front-page-footer.vue'
import Navbar from '@/views/front-pages/front-page-navbar.vue'
import CarsBanner from '@/views/front-pages/landing-page/cars-banner.vue'
import CustomersReview from '@/views/front-pages/landing-page/customers-review.vue'
import FaqSection from '@/views/front-pages/landing-page/faq-section.vue'
import Features from '@/views/front-pages/landing-page/features.vue'
import GalleryPreview from '@/views/front-pages/landing-page/gallery-preview.vue'
import PricingPlans from '@/views/front-pages/landing-page/pricing-plans.vue'
import WhatIDo from '@/views/front-pages/landing-page/what-i-do.vue'
import { useConfigStore } from '@core/stores/config'

const store = useConfigStore()

store.skin = 'default'
definePageMeta({
  layout: 'blank',
  public: true,

})

const activeSectionId = ref()

const refHome = ref()
const refServices = ref()
const refPortfolio = ref()
const refAbout = ref()
const refReferences = ref()
const refContact = ref()

useIntersectionObserver(
  [refHome, refServices, refPortfolio, refAbout, refReferences, refContact],
  ([{ isIntersecting, target }]) => {
    if (isIntersecting)
      activeSectionId.value = target.id
  },
  {
    threshold: 0.25,
  },
)
</script>

<template>
  <div class="landing-page-wrapper">
    <Navbar :active-id="activeSectionId" />

    <CarsBanner ref="refHome" />

    <!-- Que se hace -->
    <WhatIDo />

    <!-- 👉 Portafolio -->
    <div :style="{ 'background-color': 'rgb(var(--v-theme-surface))' }">
      <PricingPlans ref="refPortfolio" />
    </div>

    <!-- 👉 Servicios -->
    <div :style="{ 'background-color': 'rgb(var(--v-theme-surface))' }">
      <Features ref="refServices" />
    </div>

    <!-- 👉 Sobre mí + Timeline -->
    <div :style="{ 'background-color': 'rgb(var(--v-theme-surface))' }">
      <FaqSection ref="refAbout" />
    </div>

    <!-- 👉 Galería -->
    <GalleryPreview />

    <!-- 👉 Referencias -->
    <div :style="{ 'background-color': 'rgb(var(--v-theme-surface))' }">
      <CustomersReview ref="refReferences" />
    </div>

    <!-- 👉 Footer & Contacto -->
    <Footer ref="refContact" />
  </div>
</template>

<style lang="scss">
@media (max-width: 960px) and (min-width: 600px) {
  .landing-page-wrapper {
    .v-container {
      padding-inline: 2rem !important;
    }
  }
}
</style>
