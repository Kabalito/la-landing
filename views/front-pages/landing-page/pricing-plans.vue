<script setup lang="ts">
import { useDisplay } from 'vuetify'
import desing from '@images/moks/desing.png'
import godriveview from '@images/moks/godrive.png'
import papediview from '@images/moks/papediweb.png'
import xcoreview from '@images/moks/xcoreview.png'

const display = useDisplay()
const filters = ['Todo', 'Desarrollo Web', 'Diseño Gráfico']
const activeFilter = ref('Todo')
const comparisonValue = ref(55)

const projects = [
  {
    title: 'Master Tecnocam / Xcore Fit',
    category: 'Desarrollo Web',
    desc: 'Sistema administrativo con gestión de datos complejos y paneles en tiempo real.',
    tags: ['Vue.js', 'TypeScript', 'Dashboards'],
    github: 'https://github.com/',
    url: 'https://xcore.fit/',
    img: xcoreview,
  },
  {
    title: 'Papedi Delivery App',
    category: 'Desarrollo Web',
    desc: 'Web App con manejo de estado en tiempo real (Socket.IO) y geolocalización.',
    tags: ['Vue.js', 'Socket.IO', 'Geo'],
    github: 'https://github.com/',
    url: 'https://www.papedidelivery.com/',
    img: papediview,
  },
  {
    title: 'GODRIVE - Conduce a tu manera.',
    category: 'Desarrollo Web',
    desc: 'Renta un auto de manera rápida y sencilla con nuestra plataforma intuitiva.',
    tags: ['Nuxt 3', 'Forms', 'UX'],
    img: godriveview,
    url: 'https://godrive.rent/',
  },
  {
    title: 'Branding & Material Publicitario',
    category: 'Diseño Gráfico',
    desc: 'Logotipos, piezas promocionales y diseño multimedia para marcas locales.',
    tags: ['Branding', 'Identidad', 'Print'],
    img: desing,
  },
  {
    title: 'Comparación Boceto vs Resultado',
    category: 'Diseño Gráfico',
    desc: 'Desliza para ver el proceso creativo desde el boceto hasta el resultado final.',
    tags: ['Proceso', 'UI', 'Logo'],
    type: 'comparison',
    img: xcoreview,
  },
]

const filteredProjects = computed(() => {
  if (activeFilter.value === 'Todo')
    return projects

  return projects.filter(project => project.category === activeFilter.value)
})
</script>

<template>
  <div id="portfolio">
    <VContainer>
      <div class="portfolio-section">
        <div class="headers text-center">
          <VChip
            label
            color="primary"
            class="mb-3 mb-sm-4"
            :size="display.xs ? 'small' : 'default'"
          >
            Portafolio
          </VChip>

          <h4 class="d-flex align-center justify-center flex-wrap mb-2 mb-sm-3">
            <span class="text-h4 text-md-h3 text-lg-h2 font-weight-bold me-2">
              Proyectos que combinan
            </span>
            <span class="text-primary font-weight-black text-h4 text-md-h3 text-lg-h2">
              código y diseño
            </span>
          </h4>

          <p class="text-body-1 text-sm-h6 mx-auto">
            Selecciona una categoría para ver mis trabajos más recientes.
          </p>
        </div>

        <div class="d-flex justify-center mt-6 mt-sm-8">
          <VBtnToggle
            v-model="activeFilter"
            mandatory
            divided
            color="primary"
            variant="tonal"
            class="filters-toggle"
          >
            <VBtn
              v-for="filter in filters"
              :key="filter"
              :value="filter"
            >
              {{ filter }}
            </VBtn>
          </VBtnToggle>
        </div>

        <VRow class="mt-8">
          <VCol
            v-for="(project, index) in filteredProjects"
            :key="index"
            cols="12"
            md="6"
            lg="4"
          >
            <VCard
              class="portfolio-card h-100"
              :elevation="display.xs ? 2 : 6"
              :ripple="false"
            >
              <div class="portfolio-media">
                <template v-if="project.type === 'comparison'">
                  <div class="comparison-frame">
                    <div class="comparison-before" />
                    <div
                      class="comparison-after"
                      :style="{ width: `${comparisonValue}%` }"
                    />
                    <div
                      class="comparison-handle"
                      :style="{ left: `${comparisonValue}%` }"
                    />
                  </div>
                  <input
                    v-model="comparisonValue"
                    type="range"
                    min="15"
                    max="85"
                    class="comparison-range"
                  >
                </template>
                <template v-else>
                  <a
                    v-if="project.url"
                    class="media-link"
                    :href="project.url"
                    target="_blank"
                    rel="noopener noreferrer"
                  >
                    <div class="loop-badge">
                      <VIcon icon="tabler-player-play" />
                      <span>Visitar...</span>
                    </div>
                    <div class="media-text">
                      <VImg
                        :src="project.img"
                        :alt="project.title"
                        :width="600"
                        aspect-ratio="16/9"
                        cover
                      />
                    </div>
                  </a>
                  <div v-else>
                    <div class="loop-badge">
                      <VIcon icon="tabler-player-play" />
                      <span>Visitar...</span>
                    </div>
                    <div class="media-text">
                      <VImg
                        :src="project.img"
                        :alt="project.title"
                        :width="600"
                        aspect-ratio="16/9"
                        cover
                      />
                    </div>
                  </div>
                </template>
              </div>

              <VCardText class="pa-5">
                <div class="text-caption text-primary font-weight-semibold mb-2">
                  {{ project.category }}
                </div>
                <h5 class="text-h6 font-weight-bold mb-2">
                  {{ project.title }}
                </h5>
                <p class="text-body-2 mb-4">
                  {{ project.desc }}
                </p>

                <div class="d-flex flex-wrap gap-2 mb-4">
                  <VChip
                    v-for="(tag, tagIndex) in project.tags"
                    :key="tagIndex"
                    size="x-small"
                    label
                    color="primary"
                    variant="tonal"
                  >
                    {{ tag }}
                  </VChip>
                </div>
                <!--
                  <VBtn
                  v-if="project.github"
                  :href="project.github"
                  target="_blank"
                  rel="noopener noreferrer"
                  variant="outlined"
                  size="small"
                  >
                  Ver en GitHub
                  </VBtn>
                -->
              </VCardText>
            </VCard>
          </VCol>
        </VRow>
      </div>
    </VContainer>
  </div>
</template>

<style lang="scss" scoped>
#portfolio {
  position: relative;
  overflow: hidden;
  border-radius: 3.75rem;
  background-color: rgb(var(--v-theme-background));

  @media (max-width: 599px) {
    border-radius: 2rem;
  }

  &::before {
    position: absolute;
    background:
      linear-gradient(
        90deg,
        transparent 0%,
        rgba(var(--v-theme-primary), 0.2) 50%,
        transparent 100%
      );
    block-size: 1px;
    content: "";
    inset-block-start: 0;
    inset-inline: 0;
  }
}

.portfolio-section {
  margin-block: 4rem;
  margin-inline: 0;

  @media (min-width: 600px) {
    margin-block: 5rem;
  }

  @media (min-width: 960px) {
    margin-block: 6rem;
  }
}

.headers {
  margin-inline: auto;
  max-inline-size: 800px;

  .v-chip {
    padding-block: 0.5rem;
    padding-inline: 1.25rem;

    @media (max-width: 599px) {
      padding-block: 0.375rem;
      padding-inline: 1rem;
    }
  }
}

.portfolio-card {
  overflow: hidden;
  border: 1px solid rgba(var(--v-theme-on-background), 0.08);
  border-radius: 20px;
  transition: transform 0.3s ease, box-shadow 0.3s ease;

  &:hover {
    box-shadow: 0 18px 36px rgba(var(--v-theme-primary), 0.12) !important;
    transform: translateY(-6px);
  }
}

.portfolio-media {
  position: relative;
  display: flex;
  overflow: hidden;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, rgba(var(--v-theme-primary), 0.2), rgba(var(--v-theme-primary), 0.05));
  block-size: 190px;
}

.loop-badge {
  position: absolute;
  z-index: 2;
  display: flex;
  align-items: center;
  border-radius: 999px;
  background: rgba(var(--v-theme-surface), 0.9);
  font-size: 0.75rem;
  font-weight: 600;
  gap: 0.35rem;
  inset-block-start: 12px;
  inset-inline-end: 12px;
  padding-block: 0.25rem;
  padding-inline: 0.75rem;
}

.media-text {
  font-weight: 600;
  opacity: 0.6;
}

.media-link {
  display: block;
  block-size: 100%;
  color: inherit;
  cursor: pointer;
  inline-size: 100%;
  text-decoration: none;
}

.comparison-frame {
  position: relative;
  overflow: hidden;
  border-radius: 16px;
  background: rgba(var(--v-theme-background), 0.6);
  block-size: 140px;
  inline-size: 85%;
}

.comparison-before,
.comparison-after {
  position: absolute;
  inset: 0;
}

.comparison-before {
  background:
    repeating-linear-gradient(
      45deg,
      rgba(var(--v-theme-on-surface), 0.05),
      rgba(var(--v-theme-on-surface), 0.05) 6px,
      transparent 6px,
      transparent 12px
    );
}

.comparison-after {
  background: linear-gradient(120deg, rgba(var(--v-theme-primary), 0.35), rgba(var(--v-theme-primary), 0.05));
}

.comparison-handle {
  position: absolute;
  background: rgba(var(--v-theme-primary), 0.6);
  inline-size: 2px;
  inset-block: 0;
  transform: translateX(-1px);
}

.comparison-range {
  inline-size: 80%;
  margin-block-start: 0.75rem;
}

.filters-toggle {
  display: inline-flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.filters-toggle :deep(.v-btn) {
  justify-content: center;
  min-inline-size: 140px;
}
</style>
