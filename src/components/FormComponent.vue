<script setup>
const text = defineModel();
const emit = defineEmits(["submit"]);

const submit = (event) => {
  emit("submit", event, text.value);
};
</script>
<template>
  <form
    class="w-full flex justify-center items-center"
    @submit.prevent.enter="submit"
  >
    <input
      class="block max-w-150 w-full bg-white/5 h-10 p-4 rounded-full text-white"
      type="search"
      name=""
      placeholder="Search Pokémon..."
      v-model.trim="text"
    />
  </form>
</template>

<style scoped></style>
