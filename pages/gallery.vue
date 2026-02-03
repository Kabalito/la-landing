<script setup lang="ts">
import GallerySection from '@/components/gallery/GallerySection.vue'
import Footer from '@/views/front-pages/front-page-footer.vue'
import Navbar from '@/views/front-pages/front-page-navbar.vue'
import { useConfigStore } from '@core/stores/config'

const store = useConfigStore()

store.skin = 'default'

definePageMeta({
  layout: 'blank',
  public: true,
})
</script>

<template>
  <div class="gallery-page-wrapper">
    <Navbar />
    <GallerySection />
    <Footer />
  </div>
</template>

<style lang="scss" scoped>
.gallery-page-wrapper {
  background: rgb(var(--v-theme-surface));
}
</style>
