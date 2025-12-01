<script setup>
const { text } = defineProps(["text"]);
</script>

<template class="w-100 flex justify-center items-center">
  <button>{{ text.charAt(0).toUpperCase() + text.slice(1) }}</button>
</template>

<style scoped></style>
