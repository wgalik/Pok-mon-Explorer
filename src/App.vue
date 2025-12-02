<script setup>
import logoBall from "./assets/poke-ball.png";

import { ref, computed } from "vue";
import FormComponent from "./components/FormComponent.vue";
import ButtonComponent from "./components/ButtonComponent.vue";
import PokemonCard from "./components/PokemonCard.vue";

const limit = ref(6);
const pokemonList = ref([]);
const gotData = ref(false);

const typeColors = {
  normal: "#A8A77A",
  fire: "#EE8130",
  water: "#6390F0",
  electric: "#F7D02C",
  grass: "#7AC74C",
  ice: "#96D9D6",
  fighting: "#C22E28",
  poison: "#A33EA1",
  ground: "#E2BF65",
  flying: "#A98FF3",
  psychic: "#F95587",
  bug: "#A6B91A",
  rock: "#B6A136",
  ghost: "#735797",
  dragon: "#6F35FC",
  dark: "#705746",
  steel: "#B7B7CE",
  fairy: "#D685AD",
};

const list = computed(() => pokemonList.value.slice(0, limit.value));

const getData = (search) => {
  const API = `https://pokeapi.co/api/v2/type/${search}`;
  pokemonList.value = [];
  fetch(API)
    .then((response) => {
      if (response.ok) {
        return response;
      }
    })
    .then((response) => response.json())
    .then((data) => {
      pokemonList.value = data.pokemon;
      gotData.value = true;
    });
};

const buttonHandler = (e) => {
  e.target.classList.toggle("active");
  if (!e.target.classList.contains("active")) return;
  const search = e.target.id;
  getData(search);
};

const submit = (e, text) => {
  if (!text) return;
  const search = text;
  getData(search);
};

const loadMore = () => (limit.value += 12);
</script>

<template>
  <header class="flex flex-col justify-center items-center w-full">
    <h1 class="my-8 font-bold text-orange-400 text-4xl text-center">
      <img :src="logoBall" class="w-10 aspect-square inline-block align-top" />
      Pokémon Explorer
    </h1>
    <FormComponent @submit="submit" />
  </header>
  <main class="w-full grid gap-4">
    <section class="w-full flex justify-center items-center flex-wrap gap-4">
      <ButtonComponent
        type="button"
        v-for="(value, key) in typeColors"
        :key="value"
        :id="key"
        :style="{ backgroundColor: value }"
        :text="key"
        @click="buttonHandler"
      />
    </section>

    <section v-if="gotData" class="w-full grid grid-cols-3 gap-4">
      <PokemonCard
        v-for="pokemon in list"
        :name="pokemon.pokemon.name"
        :url="pokemon.pokemon.url"
        :key="pokemon.pokemon.name"
        :typeColors
      />
    </section>
    <button
      v-if="gotData"
      type="button"
      @click="loadMore"
      class="grid w-40 px-4 py-1 font-bold text-white text-lg rounded-full border-2 bg-blue-500 border-[#121212] hover:bg-white hover:text-black active:outline-2 transition duration-300 ease-in-out cursor-pointer justify-self-center"
    >
      Load More
    </button>
  </main>
</template>
<style scoped>
.active {
  outline: 1px solid white;
}
</style>
