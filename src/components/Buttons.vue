<script setup lang="ts">
defineProps<{
  text: string
  mode: string
}>()
</script>

<template>
  <button class="btn btn-warning w-[25%] m-4 py-4" :class="mode == 'selected' ? 'btn-active' : 'btn-outline'">{{ text
  }}</button>
</template>

<style scoped></style>
