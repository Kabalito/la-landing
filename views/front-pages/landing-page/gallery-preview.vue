<script setup lang="ts">
interface GalleryPreviewItem {
  folder: string
  file: string
  title: string
  description: string
}

const previewItems: GalleryPreviewItem[] = [
  {
    folder: 'desarrollo-web',
    file: '1.png',
    title: 'Xcore Web - Dashboard',
    description: 'Panel de gestión con métricas y reportes.',
  },
  {
    folder: 'desarrollo-web',
    file: '2.png',
    title: 'Xcore Web - Clientes',
    description: 'Control de usuarios, planes y pagos.',
  },
  {
    folder: 'mobil',
    file: '1.png',
    title: 'App Delivery',
    description: 'Experiencia móvil con seguimiento en tiempo real.',
  },
  {
    folder: 'flyers',
    file: '1.png',
    title: 'Taco Express',
    description: 'Flyer promocional para restaurante.',
  },
  {
    folder: 'logos',
    file: '1.png',
    title: 'Xcore',
    description: 'Branding para sistema fitness.',
  },
  {
    folder: 'logos',
    file: '2.png',
    title: 'Vikingo',
    description: 'Identidad visual para bar & restaurante.',
  },
]

const galleryImages = import.meta.glob('../../../assets/gallery/**/*.{png,jpg,jpeg,webp,avif}', {
  eager: true,
  import: 'default',
})

const resolveImage = (folder: string, file: string) => {
  const match = Object.entries(galleryImages).find(([path]) => path.endsWith(`/gallery/${folder}/${file}`))

  return (match?.[1] as string) || ''
}
</script>

<template>
  <section class="gallery-preview py-12">
    <VContainer>
      <div class="text-center mb-8">
        <h2 class="text-h4 mb-3">
          Algunos de mis diseños y desarrollos recientes
        </h2>
        <p class="text-body-1 text-medium-emphasis">
          Desde interfaces web hasta identidad visual, cada proyecto refleja mi compromiso con la calidad y el detalle.
        </p>
      </div>

      <VRow>
        <VCol
          v-for="item in previewItems"
          :key="`${item.folder}-${item.file}`"
          cols="12"
          sm="6"
          md="4"
        >
          <VCard
            class="gallery-preview-card"
            elevation="2"
          >
            <VImg
              :src="resolveImage(item.folder, item.file)"
              height="220"
              cover
            />
            <VCardText>
              <div class="text-subtitle-1 font-weight-medium">
                {{ item.title }}
              </div>
              <div class="text-body-2 text-medium-emphasis">
                {{ item.description }}
              </div>
            </VCardText>
          </VCard>
        </VCol>
      </VRow>

      <div class="d-flex flex-column align-center text-center mt-10">
        <p class="text-body-1 text-medium-emphasis mb-4">
          ¿Quieres ver más proyectos y categorías? Explora la galería completa.
        </p>
        <VBtn
          color="primary"
          to="/gallery"
        >
          Ver galería completa
        </VBtn>
      </div>
    </VContainer>
  </section>
</template>

<style lang="scss" scoped>
.gallery-preview {
  background-color: rgb(var(--v-theme-surface));
}

.gallery-preview-card {
  transition: transform 0.2s ease, box-shadow 0.2s ease;

  &:hover {
    box-shadow: 0 14px 32px rgba(15, 23, 42, 12%);
    transform: translateY(-4px);
  }
}
</style>
