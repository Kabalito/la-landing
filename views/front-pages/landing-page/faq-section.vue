<script setup lang="ts">
import profile from '@images/profile.png'

const timeline = [
  {
    period: '2023 - 2025',
    title: 'Frontend Developer en Soluciones Tecnocam',
    subtitle: 'Presencial',
  },
  {
    period: '2022 - 2023',
    title: 'Dev Vue.js en Tecnología Educativa Pérez',
    subtitle: 'Presencial',
  },
  {
    period: '2022 - Presente',
    title: 'Frontend Dev en Papedi C.A',
    subtitle: 'Remoto',
  },
  {
    period: '2016 - Presente',
    title: 'Diseñador Gráfico Senior & Freelance',
    subtitle: 'Branding & Multimedia',
  },
]
</script>

<template>
  <div id="about">
    <VContainer>
      <div class="about-section">
        <div class="headers d-flex justify-center flex-column align-center text-center mb-12">
          <VChip
            label
            color="primary"
            size="small"
            class="px-4"
            style="border-radius: 20px;"
          >
            <VIcon
              icon="tabler-user"
              size="16"
            />
            Sobre mí
          </VChip>

          <h2 class="text-h3 font-weight-bold mb-4">
            Soy Luis Amaya,
            <span class="text-primary position-relative">
              diseñador y developer.
              <div class="underline-effect" />
            </span>
          </h2>

          <p class="text-body-1 mb-0 max-width-700">
            Soy Luis Amaya, radicado en San Juan de los Morros. Comencé en el diseño gráfico en 2016 y evolucioné hacia el código, lo que me permite construir interfaces que no solo se ven bien, sino que están perfectamente optimizadas.
          </p>
        </div>

        <VRow class="align-start">
          <VCol
            cols="12"
            lg="5"
          >
            <VCard
              class="about-image-card mb-6"
              elevation="6"
            >
              <VImg
                :src="profile"
                alt="Luis Amaya"
                height="620"
                cover
              />
            </VCard>
            <VCard
              class="about-card"
              elevation="6"
            >
              <VCardText class="pa-6">
                <div class="d-flex flex-column gap-4">
                  <div class="d-flex align-start gap-3">
                    <VAvatar
                      color="primary"
                      variant="tonal"
                    >
                      <VIcon icon="tabler-rocket" />
                    </VAvatar>
                    <div>
                      <h4 class="text-h6 font-weight-bold mb-1">
                        Enfoque en resultados
                      </h4>
                      <p class="text-body-2 mb-0">
                        Proyectos orientados a ventas, conversión y eficiencia.
                      </p>
                    </div>
                  </div>
                  <div class="d-flex align-start gap-3">
                    <VAvatar
                      color="primary"
                      variant="tonal"
                    >
                      <VIcon icon="tabler-stack-2" />
                    </VAvatar>
                    <div>
                      <h4 class="text-h6 font-weight-bold mb-1">
                        Stack sólido
                      </h4>
                      <p class="text-body-2 mb-0">
                        Vue.js, TypeScript, UX research y diseño visual.
                      </p>
                    </div>
                  </div>
                  <div class="d-flex align-start gap-3">
                    <VAvatar
                      color="primary"
                      variant="tonal"
                    >
                      <VIcon icon="tabler-users" />
                    </VAvatar>
                    <div>
                      <h4 class="text-h6 font-weight-bold mb-1">
                        Trabajo en equipo
                      </h4>
                      <p class="text-body-2 mb-0">
                        Colaboración con equipos multidisciplinarios y remotos.
                      </p>
                    </div>
                  </div>
                </div>
              </VCardText>
            </VCard>
          </VCol>

          <VCol
            cols="12"
            lg="7"
          >
            <div class="timeline">
              <div
                v-for="(item, index) in timeline"
                :key="index"
                class="timeline-item"
              >
                <div class="timeline-dot" />
                <div class="timeline-content">
                  <div class="text-caption text-primary font-weight-semibold mb-1">
                    {{ item.period }}
                  </div>
                  <h4 class="text-h6 font-weight-bold mb-1">
                    {{ item.title }}
                  </h4>
                  <p class="text-body-2 mb-0">
                    {{ item.subtitle }}
                  </p>
                </div>
              </div>
            </div>
          </VCol>
        </VRow>
      </div>
    </VContainer>
  </div>
</template>

<style lang="scss" scoped>
#about {
  position: relative;
  overflow: hidden;
  border-radius: 48px 48px 0 0;
  background:
    linear-gradient(
      135deg,
      rgba(var(--v-theme-background), 0.95) 0%,
      rgba(var(--v-theme-surface), 0.98) 100%
    );

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

.about-section {
  position: relative;
  z-index: 1;
  margin-block: 6rem;
}

.max-width-700 {
  margin-inline: auto;
  max-inline-size: 700px;
}

.text-primary {
  position: relative;
  display: inline-block;

  .underline-effect {
    position: absolute;
    z-index: -1;
    border-radius: 3px;
    background: rgba(var(--v-theme-primary), 0.15);
    block-size: 6px;
    inset-block-end: 2px;
    inset-inline: 0;
  }
}

.about-card {
  border: 1px solid rgba(var(--v-theme-primary), 0.12);
  border-radius: 20px;
}

.about-image-card {
  overflow: hidden;
  border: 1px solid rgba(var(--v-theme-primary), 0.12);
  border-radius: 20px;
}

.timeline {
  position: relative;
  padding-inline-start: 1.5rem;
}

.timeline::before {
  position: absolute;
  background: rgba(var(--v-theme-primary), 0.2);
  block-size: 100%;
  content: "";
  inline-size: 2px;
  inset-block-start: 0;
  inset-inline-start: 0.5rem;
}

.timeline-item {
  position: relative;
  display: flex;
  gap: 1.5rem;
  padding-block: 0.5rem 1.75rem;
}

.timeline-dot {
  position: absolute;
  border-radius: 50%;
  background: rgb(var(--v-theme-primary));
  block-size: 12px;
  inline-size: 12px;
  inset-block-start: 0.75rem;
  inset-inline-start: 0.18rem;
}

.timeline-content {
  border-radius: 16px;
  background: rgba(var(--v-theme-surface), 0.85);
  inline-size: 100%;
  padding-block: 1rem;
  padding-inline: 1.25rem;
}

@media (max-width: 599px) {
  #about {
    border-radius: 32px 32px 0 0;
  }

  .about-section {
    margin-block: 3rem;
  }

  .headers h2 {
    font-size: 28px !important;
  }
}

@media (min-width: 1920px) {
  .about-section {
    margin-inline: auto;
    max-inline-size: 1600px;
  }
}
</style>
