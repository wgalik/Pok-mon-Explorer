<script setup>
const { text } = defineProps(["text"]);
</script>

<template class="">
  <button class=" px-2 text-white rounded-full border-2 border-[#121212] text-sm cursor-pointer" >{{ text.charAt(0).toUpperCase() + text.slice(1) }}</button>
</template>

<style scoped></style>
