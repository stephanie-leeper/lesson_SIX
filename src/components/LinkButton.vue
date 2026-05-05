<script setup lang="ts">
defineProps<{
  label: string
  url: string
  icon: string
}>()
</script>

<template>
  <v-btn
    :href="url"
    target="_blank"
    rel="noopener noreferrer"
    variant="tonal"
    size="large"
    block
    rounded="lg"
    class="link-button justify-start text-none"
  >
    <template #prepend>
      <v-avatar size="28" color="primary" class="mx-3">
        <v-icon size="18" :icon="icon" />
      </v-avatar>
    </template>
    {{ label }}
  </v-btn>
</template>

<style scoped>
.link-button {
  transition:
    transform 0.2s ease,
    box-shadow 0.2s ease,
    background-color 0.2s ease;
}

.link-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.12);
}

.link-button:active {
  transform: translateY(0);
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
}
</style>
