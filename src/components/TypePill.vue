<script setup>
const { pill } = defineProps(["pill"]);
</script>

<template>
  <span class="bg-white/25 px-4 rounded-full text-sm">{{ pill.charAt(0).toUpperCase() + pill.slice(1)  }}</span>
</template>

<style scoped></style>
