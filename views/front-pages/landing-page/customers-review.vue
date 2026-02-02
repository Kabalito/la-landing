<script setup lang="ts">
import { register } from 'swiper/element/bundle'
import { ref } from 'vue'
import { useDisplay } from 'vuetify'
import avatar1 from '@images/review/1.png'
import avatar2 from '@images/review/2.png'
import avatar3 from '@images/review/3.png'
import avatar4 from '@images/review/4.png'
import avatar5 from '@images/review/5.png'
import avatar6 from '@images/review/6.png'

register()

const display = useDisplay()

const reviewData = [
  {
    desc: 'Trabajar con Luis garantiza calidad de código y estética. Entendió el negocio y lo tradujo a una interfaz clara y veloz.',
    rating: 5,
    name: 'Igor Piedra',
    position: 'Backend Lead',
    avatar: avatar2,
    location: 'Colaboración en producto digital',
  },
  {
    desc: 'Luis combina lógica y diseño con una ejecución impecable. Siempre entrega más allá de lo esperado.',
    rating: 5,
    name: 'Russell Hasson',
    position: 'Full Stack',
    avatar: avatar4,
    location: 'Colaboración en proyectos web',
  },
  {
    desc: 'Excelente profesional, comprometido y detallista. Su trabajo en frontend y UI mejoró significativamente la experiencia del usuario.',
    rating: 5,
    name: 'Jose Perez',
    position: 'Dirección de Ventas',
    avatar: avatar6,
    location: 'Sector Empresarial',
  },
  {
    desc: 'Luis fue un compañero de trabajo excepcional: comunicativo, proactivo y siempre dispuesto a apoyar al equipo.',
    rating: 5,
    name: 'Alexis Gonsalez',
    position: 'Frontend Engineer',
    avatar: avatar1,
    location: 'Trabajo en equipo multidisciplinario',
  },
  {
    desc: 'Su colaboración elevó la calidad del proyecto; aportó soluciones claras y mantuvo un ambiente de trabajo positivo.',
    rating: 5,
    name: 'Miguel Flores',
    position: 'Backend Senior',
    avatar: avatar5,
    location: 'Proyecto web en sprint ágil',
  },
  {
    desc: 'Gran compañero de trabajo y líder técnico cuando se necesitaba. Siempre cumplió tiempos y cuidó los detalles.',
    rating: 5,
    name: 'Nelson Yeguez',
    position: 'Backend Developer',
    avatar: avatar3,
    location: 'Desarrollo de plataforma Administrativa',
  },
]

const customerReviewSwiper = ref(null)
const activeReviewIndex = ref(0)

const slide = (dir: string) => {
  const swiper = customerReviewSwiper.value?.swiper

  if (dir === 'prev')
    swiper.slidePrev()
  else
    swiper.slideNext()
}

const stats = [
  { value: '7+', label: 'Años de experiencia' },
  { value: '20+', label: 'Proyectos entregados' },
  { value: '30+', label: 'Marcas apoyadas' },
  { value: '100%', label: 'Enfoque en resultados' },
]
</script>

<template>
  <div
    id="references"
    class="position-relative"
  >
    <div class="customer-reviews">
      <VContainer>
        <div class="headers text-center text-md-start">
          <VChip
            label
            color="primary"
            class="mb-3 mb-sm-4"
            :size="display.xs ? 'small' : 'default'"
          >
            <VIcon
              icon="tabler-star"
              size="16"
              class="me-1"
            />
            Referencias
          </VChip>

          <div class="d-md-flex align-end justify-space-between mb-6 mb-sm-8 mb-md-10">
            <div>
              <h2 class="d-flex align-center flex-wrap mb-2 mb-sm-3">
                <span class="text-h4 text-md-h3 text-lg-h2 font-weight-bold me-2">
                  Qué dicen
                </span>
                <span class="text-primary text-h4 text-md-h3 text-lg-h2 font-weight-bold">
                  colaboradores y clientes
                </span>
              </h2>
              <p class="text-body-1 text-sm-h6 text-medium-emphasis">
                Comentarios reales sobre proyectos donde se combinó diseño, producto y performance.
              </p>
            </div>

            <div class="d-none d-md-flex align-center gap-3 mt-4 mt-md-0">
              <VBtn
                icon
                variant="tonal"
                size="small"
                @click="slide('prev')"
              >
                <VIcon icon="tabler-chevron-left" />
              </VBtn>
              <VBtn
                icon
                variant="tonal"
                size="small"
                @click="slide('next')"
              >
                <VIcon icon="tabler-chevron-right" />
              </VBtn>
            </div>
          </div>
        </div>

        <div class="testimonials-carousel-wrapper position-relative">
          <ClientOnly>
            <swiper-container
              ref="customerReviewSwiper"
              :slides-per-view="1"
              :space-between="24"
              events-prefix="swiper-"
              :loop="true"
              :centered-slides="display.xs"
              :breakpoints="{
                600: { slidesPerView: 2, spaceBetween: 24 },
                960: { slidesPerView: 3, spaceBetween: 32 },
                1280: { slidesPerView: 3, spaceBetween: 40 },
              }"
              @swiper-slide-change="(e) => activeReviewIndex = e.detail[0].activeIndex"
            >
              <swiper-slide
                v-for="(data, index) in reviewData"
                :key="index"
              >
                <VCard
                  class="testimonial-card h-100"
                  :elevation="display.xs ? 2 : 6"
                  :ripple="false"
                >
                  <VCardText class="pa-4 pa-sm-6">
                    <div class="d-flex justify-space-between align-start mb-3 mb-sm-4">
                      <VRating
                        :model-value="data.rating"
                        color="warning"
                        density="compact"
                        readonly
                        :size="display.xs ? 'small' : 'default'"
                      />
                      <VIcon
                        icon="tabler-quote"
                        size="32"
                        color="rgba(var(--v-theme-primary), 0.1)"
                      />
                    </div>

                    <p class="text-body-2 text-sm-body-1 mb-4 mb-sm-5">
                      "{{ data.desc }}"
                    </p>

                    <div class="d-flex align-center gap-x-3">
                      <VAvatar
                        :image="data.avatar"
                        :size="display.xs ? 40 : 48"
                        class="avatar-border"
                      />
                      <div class="flex-grow-1">
                        <h6 class="text-h6 text-sm-h5 font-weight-bold mb-0">
                          {{ data.name }}
                        </h6>
                        <div class="d-flex flex-wrap align-center gap-1 gap-sm-2">
                          <span class="text-caption text-sm-body-2 text-medium-emphasis">
                            {{ data.position }}
                          </span>
                          <span class="text-caption text-sm-body-2 text-disabled d-none d-sm-inline">
                            •
                          </span>
                          <span class="text-caption text-sm-body-2 text-disabled">
                            {{ data.location }}
                          </span>
                        </div>
                      </div>
                    </div>
                  </VCardText>
                </VCard>
              </swiper-slide>
            </swiper-container>
          </ClientOnly>

          <div class="d-flex d-md-none justify-center align-center gap-4 mt-6">
            <VBtn
              icon
              variant="tonal"
              size="small"
              @click="slide('prev')"
            >
              <VIcon icon="tabler-chevron-left" />
            </VBtn>

            <div class="d-flex gap-2">
              <div
                v-for="(_, index) in reviewData"
                :key="index"
                class="carousel-indicator"
                :class="{ active: activeReviewIndex % reviewData.length === index }"
              />
            </div>

            <VBtn
              icon
              variant="tonal"
              size="small"
              @click="slide('next')"
            >
              <VIcon icon="tabler-chevron-right" />
            </VBtn>
          </div>
        </div>

        <div class="credibility-stats mt-8 mt-sm-10 mt-md-12">
          <VRow class="justify-center">
            <VCol
              v-for="(stat, index) in stats"
              :key="index"
              cols="6"
              sm="3"
            >
              <div class="stat-card text-center">
                <div class="stat-value text-h4 text-sm-h3 font-weight-black text-primary mb-1">
                  {{ stat.value }}
                </div>
                <div class="stat-label text-body-2 text-sm-body-1 text-medium-emphasis">
                  {{ stat.label }}
                </div>
              </div>
            </VCol>
          </VRow>
        </div>
      </VContainer>
    </div>
  </div>
</template>

<style lang="scss" scoped>
#references {
  position: relative;
  overflow: hidden;
  border-radius: 3.75rem 3.75rem 0 0;
  background-color: rgb(var(--v-theme-background));

  @media (max-width: 599px) {
    border-radius: 2rem 2rem 0 0;
  }
}

.customer-reviews {
  padding-block: 4rem;

  @media (min-width: 600px) {
    padding-block: 5rem;
  }

  @media (min-width: 960px) {
    padding-block: 6rem;
  }
}

.headers {
  margin-block-end: 2rem;
  margin-inline: auto;
  max-inline-size: 800px;
}

.testimonials-carousel-wrapper {
  padding-block: 1rem;
}

.testimonial-card {
  border: 1px solid rgba(var(--v-theme-on-background), 0.08);
  border-radius: 20px;
  background: rgba(var(--v-theme-surface), 0.95);
  transition: transform 0.3s ease, box-shadow 0.3s ease;

  &:hover {
    box-shadow: 0 20px 40px rgba(var(--v-theme-primary), 8%);
    transform: translateY(-8px);
  }
}

.carousel-indicator {
  border-radius: 50%;
  background: rgba(var(--v-theme-on-surface), 0.2);
  block-size: 8px;
  inline-size: 8px;
  transition: all 0.3s ease;

  &.active {
    border-radius: 4px;
    background: rgb(var(--v-theme-primary));
    inline-size: 24px;
  }
}

.credibility-stats {
  .stat-card {
    border: 1px solid rgba(var(--v-theme-on-background), 0.05);
    border-radius: 16px;
    background: rgba(var(--v-theme-surface), 0.5);
    padding-block: 1.5rem;
    padding-inline: 1rem;
    transition: transform 0.3s ease, box-shadow 0.3s ease;

    &:hover {
      box-shadow: 0 12px 24px rgba(var(--v-theme-primary), 8%);
      transform: translateY(-2px);
    }
  }
}
</style>
