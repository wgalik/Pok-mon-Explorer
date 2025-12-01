<script setup>
import TypePill from "./typePill.vue";

import { ref, onMounted, computed } from "vue";
const { name, url, typeColors } = defineProps(["name", "url", "typeColors"]);

const pokemon = ref([]);
const pokemonTypes = ref([]);
const pokemonImage = ref([]);

const serialNumber = computed(() => {
  const match = url.match(/\/(\d+)\/?$/);
  return match[1];
});

const typeNames = computed(() => {
  return pokemonTypes.value.map((type) => type.type.name);
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
    class="grid basis-1/3 gap-2 w-full text-white card rounded-xl text-center items-center p-2"
    :style="
      typeNames.length === 1
        ? { backgroundColor: typeColors[typeNames[0]] }
        : {
            background: `linear-gradient(to right, ${
              typeColors[typeNames[0]]
            }, ${typeColors[typeNames[1]]})`,
          }
    "
  >
    <img
      :src="pokemonImage"
      alt="Pokemon image"
      srcset=""
      class="w-25 aspect-square justify-self-center"
    />
    <h2 class="text-white font-bold text-xl">
      {{ name.charAt(0).toUpperCase() + name.slice(1) }}
    </h2>

    <p class="text-white">{{ serialNumber }}</p>
    <div class="types flex flex-col sm:flex-row justify-center items gap-2">
      <TypePill
        v-for="type in pokemonTypes"
        class="text-white"
        :key="type.type.name"
        :pill="type.type.name"
      />
    </div>
  </div>
</template>

<style scoped></style>
