<script setup lang="ts">
import { computed, ref } from 'vue'

interface GalleryItemBase {
  file: string
  title: string
  description: string
  tags: string[]
  link?: string
}

interface GalleryCategory {
  key: string
  label: string
  folder: string
  items: GalleryItemBase[]
}

// 👉 Edita aquí para agregar categorías o imágenes
const categories: GalleryCategory[] = [
  {
    key: 'desarrollo-web',
    label: 'Desarrollo web',
    folder: 'desarrollo-web',
    items: [
      {
        file: '1.png',
        title: 'Xcore Web - Dashboard',
        description: 'Gestion de clientes, pagos, accesos y reportes en un software web para gimnasios.',
        tags: ['Administrar', 'Reportes', 'Clientes'],
        link: 'https://xcore.fit/',
      },
      {
        file: '2.png',
        title: 'Xcore Web - Panel Clientes',
        description: 'Gestion de clientes, pagos, accesos y reportes en un software web para gimnasios.',
        tags: ['Horarios', 'Planes', 'Clientes'],
        link: 'https://xcore.fit/',
      },
    ],
  },
  {
    key: 'mobil',
    label: 'Móvil',
    folder: 'mobil',
    items: [
      {
        file: '1.png',
        title: 'App delivery',
        description: 'Aplicación móvil con flujo de compra y tracking en tiempo real.',
        tags: ['delivery', 'app', 'startup'],
        link: 'https://example.com',
      },
    ],
  },
  {
    key: 'flyers',
    label: 'Flyers',
    folder: 'flyers',
    items: [
      {
        file: '1.png',
        title: 'Taco Express',
        description: 'Venta de comida rápida.',
        tags: ['comida', 'rápida', 'restaurante'],
      },
      {
        file: '2.png',
        title: 'Saranje Store',
        description: 'Estudio de belleza y dermatología.',
        tags: ['belleza', 'dermatología', 'estética'],
      },
      {
        file: '3.png',
        title: 'Arlebeauty',
        description: 'Beauty Content & Lifestyle.',
        tags: ['beauty', 'lifestyle', 'contenido'],
      },
      {
        file: '4.png',
        title: '4x4 OffRoad',
        description: 'Evento al que asisten los mejores proveedores e importadores de equipamiento para camionetas.',
        tags: ['evento', '4x4', 'camionetas'],
      },
      {
        file: '5.png',
        title: 'Toro Motos',
        description: 'Fábrica y distribuidor de motocicletas en Venezuela.',
        tags: ['motos', 'industria', 'venezuela'],
      },
    ],
  },
  {
    key: 'logos',
    label: 'Logos',
    folder: 'logos',
    items: [
      {
        file: '1.png',
        title: 'Xcore',
        description: 'Sistema administrativo de gymnasios.',
        tags: ['branding', 'fitness', 'software'],
      },
      {
        file: '2.png',
        title: 'Vikingo',
        description: 'Bar & restaurante.',
        tags: ['gastronomía', 'restaurante', 'branding'],
      },
      {
        file: '3.png',
        title: 'Tecnocam',
        description: 'Desarrollo de software para Pymes y la industria fitness, desarrollo de apps móviles, venta e instalación de cámaras de seguridad.',
        tags: ['software', 'pymes', 'seguridad'],
      },
      {
        file: '4.png',
        title: 'SuperEmesas',
        description: 'Página web para enviar y recibir dinero en Venezuela de forma segura, confiable y conveniente.',
        tags: ['fintech', 'pagos', 'venezuela'],
      },
      {
        file: '5.png',
        title: 'Isipay',
        description: 'Plataforma digital para comprar, vender e intercambiar activos.',
        tags: ['fintech', 'activos', 'plataforma'],
      },
      {
        file: '6.png',
        title: 'GoDrive',
        description: 'Renta un auto.',
        tags: ['movilidad', 'renta', 'autos'],
      },
    ],
  },

  // {
  //   key: 'papeleria',
  //   label: 'Papelería',
  //   folder: 'papeleria',
  //   items: [
  //     {
  //       file: '1.png',
  //       title: 'Kit corporativo',
  //       description: 'Aplicación de marca en piezas institucionales.',
  //       tags: ['corporativo', 'branding', 'impresos'],
  //     },
  //   ],
  // },
]

interface GalleryItem extends GalleryItemBase {
  category: string
  categoryLabel: string
}

const selectedCategory = ref('all')
const dialog = ref(false)
const selectedItem = ref<GalleryItem | null>(null)

const galleryImages = import.meta.glob('../../assets/gallery/**/*.{png,jpg,jpeg,webp,avif}', {
  eager: true,
  import: 'default',
})

const resolveImage = (folder: string, file: string) => {
  const match = Object.entries(galleryImages).find(([path]) => path.endsWith(`/gallery/${folder}/${file}`))

  return (match?.[1] as string) || ''
}

const allItems = computed<GalleryItem[]>(() =>
  categories.flatMap(category =>
    category.items.map(item => ({
      ...item,
      category: category.folder,
      categoryLabel: category.label,
    })),
  ),
)

const filteredItems = computed(() => {
  if (selectedCategory.value === 'all')
    return allItems.value

  return allItems.value.filter(item => item.category === selectedCategory.value)
})

const openItem = (item: GalleryItem) => {
  selectedItem.value = item
  dialog.value = true
}
</script>

<template>
  <section class="gallery-section">
    <VContainer>
      <div class="text-center mb-8">
        <h1 class="text-h3 font-weight-bold mb-2">
          Galería de trabajos
        </h1>
        <p class="text-body-1 text-medium-emphasis">
          Explora proyectos por categoría. Puedes agregar más imágenes y categorías cuando quieras.
        </p>
      </div>

      <div class="d-flex flex-wrap justify-center gap-3 mb-8">
        <VChipGroup
          v-model="selectedCategory"
          selected-class="text-primary"
        >
          <VChip
            value="all"
            variant="outlined"
          >
            Todas
          </VChip>
          <VChip
            v-for="category in categories"
            :key="category.key"
            :value="category.folder"
            variant="outlined"
          >
            {{ category.label }}
          </VChip>
        </VChipGroup>
      </div>

      <VRow>
        <VCol
          v-for="item in filteredItems"
          :key="`${item.category}-${item.file}`"
          cols="12"
          sm="6"
          md="4"
          lg="3"
        >
          <VCard
            class="gallery-card"
            elevation="2"
            @click="openItem(item)"
          >
            <VImg
              :src="resolveImage(item.category, item.file)"
              height="220"
              cover
              class="cursor-pointer"
            />
            <VCardText>
              <div class="text-subtitle-1 font-weight-medium">
                {{ item.title }}
              </div>
              <div class="text-body-2 text-medium-emphasis">
                {{ item.description }}
              </div>
              <div class="d-flex flex-wrap gap-2 mt-3">
                <VChip
                  v-for="tag in item.tags"
                  :key="tag"
                  size="small"
                  variant="tonal"
                  color="primary"
                >
                  #{{ tag }}
                </VChip>
              </div>
            </VCardText>
          </VCard>
        </VCol>
      </VRow>

      <VDialog
        v-model="dialog"
        max-width="900"
      >
        <VCard v-if="selectedItem">
          <VImg
            :src="resolveImage(selectedItem.category, selectedItem.file)"
            cover
          />
          <VCardTitle class="pt-6">
            {{ selectedItem.title }}
          </VCardTitle>
          <VCardText>
            <p class="text-body-1 mb-4">
              {{ selectedItem.description }}
            </p>
            <div class="d-flex flex-wrap gap-2 mb-6">
              <VChip
                v-for="tag in selectedItem.tags"
                :key="tag"
                size="small"
                variant="tonal"
                color="primary"
              >
                #{{ tag }}
              </VChip>
            </div>
            <div class="d-flex justify-end">
              <VBtn
                v-if="selectedItem.link"
                :href="selectedItem.link"
                target="_blank"
                color="primary"
              >
                Visitar sitio
              </VBtn>
            </div>
          </VCardText>
        </VCard>
      </VDialog>
    </VContainer>
  </section>
</template>

<style lang="scss" scoped>
.gallery-section {
  padding-block: 5rem;
}

.gallery-card {
  transition: transform 0.2s ease, box-shadow 0.2s ease;

  &:hover {
    box-shadow: 0 14px 32px rgba(15, 23, 42, 12%);
    transform: translateY(-4px);
  }
}
</style>
