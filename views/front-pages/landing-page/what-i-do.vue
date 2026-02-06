<script setup lang="ts">
const featureCards = [
  {
    icon: 'tabler-device-mobile',
    title: 'Diseño Mobile First',
    description: 'Construyo tu web pensando primero en móviles, con código limpio y optimizado para una experiencia rápida y fluida.',
  },
  {
    icon: 'tabler-devices',
    title: 'Totalmente Responsive',
    description: 'Tu sitio se adapta a celulares, tablets y escritorio para que se vea perfecto en cualquier pantalla.',
  },
  {
    icon: 'tabler-bolt',
    title: 'Velocidad Optimizada',
    description: 'Me enfoco en tiempos de carga mínimos para que tus visitantes no esperen y tu web rinda al máximo.',
  },
]
</script>

<template>
  <section class="what-i-do py-12">
    <VContainer>
      <VRow justify="center">
        <VCol
          cols="12"
          md="10"
          lg="8"
          class="text-center"
        >
          <VChip
            label
            color="primary"
            class="mb-4"
            size="small"
          >
            Que Hago
          </VChip>
          <div class="d-flex text-h2 mb-2 align-center flex-wrap justify-center">
            <div class="position-relative me-2">
              <div class="section-title">
                Transformo ideas en experiencias digitales impactantes
              </div>
            </div>
          </div>
          <p class="text-body-1 text-medium-emphasis">
            Me especializo en diseño y desarrollo web para pequeñas o grandes empresas, he trabajado con personas de:
            Venezuela, Argentina, Peru, Paraguay y chile. Cada línea de código está escrita a mano para garantizar el
            mejor rendimiento, mi objetivo es construir relaciones a largo plazo y verlas crecer proyectos con el tiempo.
          </p>
        </VCol>
      </VRow>

      <VRow
        class="mt-10"
        justify="center"
      >
        <VCol
          v-for="card in featureCards"
          :key="card.title"
          cols="12"
          md="4"
        >
          <VCard
            class="service-card h-100"
            elevation="6"
          >
            <VCardText class="pa-6 d-flex flex-column gap-4">
              <VAvatar
                size="52"
                variant="tonal"
                color="primary"
              >
                <VIcon
                  :icon="card.icon"
                  size="26"
                />
              </VAvatar>

              <div>
                <h3 class="text-h6 font-weight-bold mb-2">
                  {{ card.title }}
                </h3>
                <p class="text-body-2 mb-0">
                  {{ card.description }}
                </p>
              </div>
            </VCardText>
          </VCard>
        </VCol>
      </VRow>
    </VContainer>
  </section>
</template>

<style scoped lang="scss">
.what-i-do {
  background-color: rgb(var(--v-theme-surface));
}

.service-card {
  border: 1px solid rgba(var(--v-theme-primary), 0.08);
  border-radius: 20px;
  transition: transform 0.3s ease, box-shadow 0.3s ease;

  &:hover {
    box-shadow: 0 20px 40px rgba(var(--v-theme-primary), 0.12);
    transform: translateY(-6px);
  }
}
</style>
