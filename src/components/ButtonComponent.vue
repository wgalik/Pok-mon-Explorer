<script setup>
const { text } = defineProps(["text"]);
</script>

<template class="">
  <button
    class="px-4 py-1 text-white rounded-full border-2 border-[#121212] text-sm cursor-pointer hover:scale-110 transition duration-300 ease-in-out"
  >
    {{ text.charAt(0).toUpperCase() + text.slice(1) }}
  </button>
</template>

<style scoped></style>
