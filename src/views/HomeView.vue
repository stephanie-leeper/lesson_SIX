<script setup lang="ts">
import { computed, onMounted, ref, watch } from 'vue'
import { useTheme } from 'vuetify'
import LinkButton from '@/components/LinkButton.vue'

type LinkItem = {
  label: string
  href: string
  icon: string
}

const links: LinkItem[] = [
  {
    label: 'LinkedIn',
    href: 'https://www.linkedin.com/in/stephanieleeper',
    icon: 'mdi-linkedin',
  },
  {
    label: 'Instagram',
    href: 'https://www.instagram.com/stephanieleeper',
    icon: 'mdi-instagram',
  },
  {
    label: 'Email',
    href: 'mailto:stephanie.leeper@slalom.com',
    icon: 'mdi-email-outline',
  },
]

const theme = useTheme()
const isDark = ref(false)

const currentTheme = computed(() => (isDark.value ? 'dark' : 'light'))

function toggleTheme() {
  isDark.value = !isDark.value
}

onMounted(() => {
  const stored = localStorage.getItem('theme')
  if (stored) {
    isDark.value = stored === 'dark'
  }
  theme.change(currentTheme.value)
})

watch(isDark, (dark) => {
  theme.change(dark ? 'dark' : 'light')
  localStorage.setItem('theme', dark ? 'dark' : 'light')
})
</script>

<template>
  <v-container class="fill-height" fluid>
    <v-row justify="center" align="center" no-gutters class="w-100">
      <v-col cols="12" sm="8" md="6" lg="4">
        <v-card class="pa-6 position-relative" rounded="xl" elevation="4">
          <v-btn
            class="position-absolute"
            style="top: 12px; right: 12px"
            icon
            variant="text"
            density="comfortable"
            :aria-label="isDark ? 'Switch to light mode' : 'Switch to dark mode'"
            @click="toggleTheme"
          >
            <v-icon>{{ isDark ? 'mdi-white-balance-sunny' : 'mdi-weather-night' }}</v-icon>
          </v-btn>

          <div class="d-flex flex-column align-center text-center">
            <v-avatar size="110" color="primary" class="mb-4 text-h4 font-weight-bold">
              SL
            </v-avatar>

            <h1 class="text-h5 font-weight-bold">Stephanie Leeper</h1>
            <p class="text-body-2 text-medium-emphasis mt-1 mb-0">
              Designer, builder, lifelong learner.
            </p>
          </div>

          <div class="d-flex flex-column ga-3 mt-6">
            <LinkButton
              v-for="link in links"
              :key="link.label"
              :label="link.label"
              :url="link.href"
              :icon="link.icon"
            />
          </div>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

