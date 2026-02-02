<script setup lang="ts">
const services = [
  {
    title: 'Desarrollo Frontend de Alto Nivel',
    desc: 'Aplicaciones web rápidas y escalables utilizando Vue.js (2 y 3) y TypeScript.',
    highlight: 'Integración de APIs REST y lógica de negocio compleja.',
    icon: 'tabler-code',
  },
  {
    title: 'Diseño UI & Identidad Visual',
    desc: 'Interfaces intuitivas y atractivas, desde identidad visual hasta prototipo final.',
    highlight: 'Adobe Suite (Ps, Ai, Xd).',
    icon: 'tabler-palette',
  },
  {
    title: 'Sistemas Administrativos & Dashboards',
    desc: 'Experiencia creando herramientas internas robustas y optimizadas para equipos.',
    highlight: 'Métricas, roles y flujos operativos claros.',
    icon: 'tabler-layout-dashboard',
  },
]
</script>

<template>
  <VContainer id="services">
    <div class="feature-cards">
      <div class="headers d-flex justify-center flex-column align-center mb-12">
        <VChip
          label
          color="primary"
          class="mb-4"
          size="small"
        >
          Lo que ofrezco
        </VChip>
        <div class="d-flex text-h4 mb-2 align-center flex-wrap justify-center">
          <div class="position-relative me-2">
            <div class="section-title">
              Servicios que convierten ideas en resultados
            </div>
          </div>
        </div>
        <p
          class="text-body-1 mb-0"
          style="max-inline-size: 900px; text-align: center;"
        >
          Desarrollo y diseño centrados en negocio, rendimiento y experiencia de usuario.
        </p>
      </div>

      <VRow>
        <VCol
          v-for="(service, index) in services"
          :key="index"
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
                  :icon="service.icon"
                  size="26"
                />
              </VAvatar>

              <div>
                <h3 class="text-h6 font-weight-bold mb-2">
                  {{ service.title }}
                </h3>
                <p class="text-body-2 mb-3">
                  {{ service.desc }}
                </p>
                <div class="text-caption text-primary font-weight-semibold">
                  {{ service.highlight }}
                </div>
              </div>
            </VCardText>
          </VCard>
        </VCol>
      </VRow>
    </div>
  </VContainer>
</template>

<style lang="scss" scoped>
.feature-cards {
  margin-block: 3.75rem;
}

.section-title::after {
  position: absolute;
  background: url("../../../assets/images/front-pages/icons/section-title-icon.png") no-repeat left bottom;
  background-size: contain;
  block-size: 100%;
  content: "";
  inline-size: 120%;
  inset-block-end: 0;
  inset-inline-start: -12%;
}

.section-title {
  font-size: 24px;
  font-weight: 800;
  line-height: 36px;
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
