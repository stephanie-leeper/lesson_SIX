<script setup lang="ts">
withDefaults(
  defineProps<{
    photo?: string
    borderColor?: string
    borderWidth?: string | number
  }>(),
  {
    photo: '',
    borderColor: 'primary',
    borderWidth: 4,
  },
)
</script>

<template>
  <v-avatar
    size="110"
    :color="photo ? undefined : 'primary'"
    class="profile-pic text-h4 font-weight-bold"
    :style="{
      borderStyle: 'solid',
      borderColor: `rgb(var(--v-theme-${borderColor}))`,
      borderWidth: typeof borderWidth === 'number' ? `${borderWidth}px` : borderWidth,
    }"
  >
    <v-img v-if="photo" :src="photo" alt="Profile photo" cover />
    <slot v-else>SL</slot>
  </v-avatar>
</template>
