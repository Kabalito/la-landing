<script setup lang="ts">
import footerDarkBg from '@images/front-pages/backgrounds/footer-bg-dark.png'
import footerLightBg from '@images/front-pages/backgrounds/footer-bg-light.png'

import cvPdf from '@/assets/pdf/cv.pdf'
import logo from '@images/GO.png'

import { themeConfig } from '@themeConfig'

interface Menu {
  name: string
  to: any
  isNew?: boolean
}

const footerBg = useGenerateImageVariant(footerLightBg, footerDarkBg)

const pagesList: Menu[] = [
  { name: 'Inicio', to: { path: '/', hash: '#home' } },
  { name: 'Servicios', to: { path: '/', hash: '#services' } },
  { name: 'Portafolio', to: { path: '/', hash: '#portfolio' } },
  { name: 'Sobre mí', to: { path: '/', hash: '#about' } },
  { name: 'Referencias', to: { path: '/', hash: '#references' } },
  { name: 'Contacto', to: { path: '/', hash: '#contact' } },
  { name: 'Galería', to: { path: '/gallery' } },
]
</script>

<template>
  <div
    id="contact"
    class="footer"
  >
    <div
      class="footer-top pt-11"
      :style="{ 'background-image': `url(${footerBg})` }"
    >
      <VContainer>
        <VRow>
          <!-- 👉 Footer  -->
          <VCol
            cols="12"
            md="6"
          >
            <div
              class="mb-4"
              :class="$vuetify.display.smAndDown ? 'w-100' : 'w-75'"
            >
              <div class="app-logo mb-6">
                <img
                  :src="logo"
                  alt="logo"
                  height="100"
                >
                <h1 class="app-logo-title text-white">
                  {{ themeConfig.app.title }}
                </h1>
              </div>

              <div class="mb-6 text-white-variant">
                ¿Listo para iniciar tu proyecto? Hablemos y definimos una solución enfocada en resultados.
              </div>

              <div class="d-flex flex-column gap-3 mb-6">
                <div class="d-flex align-center gap-2">
                  <VIcon
                    icon="tabler-mail"
                    size="18"
                    color="white"
                  />
                  <span class="text-body-1 text-white-variant">kabal.amaya@hotmail.com</span>
                </div>
                <div class="d-flex align-center gap-2">
                  <VIcon
                    icon="tabler-brand-whatsapp"
                    size="18"
                    color="white"
                  />
                  <a
                    class="text-body-1 text-white-variant"
                    href="https://wa.me/584128389193"
                    target="_blank"
                    rel="noopener noreferrer"
                  >
                    +58 412 838 9193
                  </a>
                </div>
              </div>

              <div class="d-flex flex-wrap gap-3">
                <VBtn
                  color="primary"
                  :href="cvPdf"
                  target="_blank"
                >
                  Descargar CV en PDF
                </VBtn>
                <VBtn
                  variant="outlined"
                  color="white"
                  href="mailto:kabal.amaya@hotmail.com"
                >
                  Hablemos
                </VBtn>
              </div>
            </div>
          </VCol>

          <!-- 👉 Demos -->
          <!--
            <VCol
            md="2"
            sm="4"
            xs="6"
            >
            <div class="footer-links">
            <h6 class="footer-title text-h6 mb-6">
            Demos
            </h6>
            <ul style="list-style: none;">
            <li
            v-for="(item, index) in demoList"
            :key="index"
            class="mb-4"
            >
            <a
            :href="item.to"
            target="_blank"
            rel="noopener noreferrer"
            :class="$vuetify.theme.current.dark ? 'text-body-1' : 'text-white-variant'"
            >
            {{ item.title }}
            </a>
            </li>
            </ul>
            </div>
            </VCol>
          -->

          <!-- 👉 Pages  -->
          <VCol
            md="3"
            sm="6"
            xs="6"
          >
            <div class="footer-links">
              <h6 class="footer-title text-h6 mb-6">
                Secciones
              </h6>
              <ul style="list-style: none;">
                <li
                  v-for="(item, index) in pagesList"
                  :key="index"
                  class="mb-4"
                >
                  <NuxtLink
                    :class="$vuetify.theme.current.dark ? 'text-body-1' : 'text-white-variant'"
                    class="me-2"
                    :to="item.to"
                  >
                    {{ item.name }}
                  </NuxtLink>
                  <template v-if="item.isNew">
                    <VChip
                      color="primary"
                      variant="elevated"
                      label
                      size="small"
                    >
                      New
                    </VChip>
                  </template>
                </li>
              </ul>
            </div>
          </VCol>

          <VCol
            md="3"
            sm="6"
            xs="6"
          >
            <div>
              <h6 class="footer-title text-h6 mb-6">
                Redes
              </h6>
              <div class="d-flex gap-4">
                <a
                  href="https://www.linkedin.com"
                  target="_blank"
                  rel="noopener noreferrer"
                >
                  <VIcon
                    icon="tabler-brand-linkedin"
                    size="28"
                    color="white"
                  />
                </a>
                <a
                  href="https://github.com"
                  target="_blank"
                  rel="noopener noreferrer"
                >
                  <VIcon
                    icon="tabler-brand-github"
                    size="28"
                    color="white"
                  />
                </a>
              </div>
            </div>
          </VCol>
        </VRow>
      </VContainer>
    </div>

    <!-- 👉 Footer Line -->
    <div class="footer-line w-100">
      <VContainer>
        <div class="d-flex justify-space-between flex-wrap gap-y-5 align-center">
          <div class="text-body-1 text-white-variant text-wrap me-4">
            &copy; {{ new Date().getFullYear() }}
            <span class="font-weight-bold ms-1 text-white">Luis Amaya</span>
            — Portafolio profesional.
          </div>
        </div>
      </VContainer>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.footer-title {
  color: rgba(255, 255, 255, 92%);
}

.footer-top {
  border-radius: 60px 60px 0 0;
  background-size: cover;
  color: #fff;
}

.footer-links {
  .text-white-variant,
  .text-body-1 {
    &:hover {
      color: #fff;
    }
  }
}

.footer-line {
  background: #282c3e;
}

.footer {
  border-radius: 50%;

  @media (min-width: 600px) and (max-width: 960px) {
    .v-container {
      padding-inline: 2rem !important;
    }
  }
}
</style>
