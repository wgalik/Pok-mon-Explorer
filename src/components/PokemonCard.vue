<script setup>
import { ref, onMounted, computed } from "vue";
const { name, url, typeColors } = defineProps(["name", "url", "typeColors"]);

const pokemon = ref([]);
const pokemonTypes = ref([]);
const pokemonImage = ref([]);

const serialNumber = computed(() => {
  const match = url.match(/\/(\d+)\/?$/);
  return match[1];
});

onMounted(() => {
  getPokemon();
});

const getPokemon = () => {
  fetch(url)
    .then((response) => {
      if (response.ok) {
        return response;
      }
    })
    .then((response) => response.json())
    .then((data) => {
      pokemon.value = data;
      pokemonTypes.value = data.types;
      pokemonImage.value = data.sprites.other["official-artwork"].front_default;
    });
};
</script>

<template>
  <div
    class="card basis-1/3 border-2 rounded-xl grid justify-center text-center p-4"
    :style="{ backgroundColor: typeColors[pokemonTypes[0]] }"
  >
    <img
      :src="pokemonImage"
      alt="Pokemon image"
      srcset=""
      class="w-12 aspect-square"
    />
    <h2 class="text-white">{{ name }}</h2>

    <p class="text-white">{{ serialNumber }}</p>
    <p v-for="type in pokemonTypes" class="text-white" :key="type.type.name">
      {{ type.type.name }}
    </p>
  </div>
</template>

<style scoped></style>
