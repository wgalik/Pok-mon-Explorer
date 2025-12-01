<script setup>
import logoBall from "./assets/poke-ball.png";

import { ref, computed } from "vue";
import ButtonComponent from "./components/ButtonComponent.vue";
import PokemonCard from "./components/PokemonCard.vue";

const limit = ref(6);
const pokemonList = ref([]);
const text = ref("");
const gotData = ref(false);
const input = defineModel();

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

const buttonHandler = (e) => {
  e.target.classList.toggle("active");
  const search = e.target.id;
  getData(search);
};

const submit = () => {
  const search = text.value;
  getData(search);
};

const loadMore = () => (limit.value += 12);
</script>

<template>
  <header class="flex flex-col justify-center items-center">
    <h1 class="my-8 font-bold text-orange-400 text-3xl text-center">
      <img :src="logoBall" class="w-9 aspect-square inline-block align-top" />
      Pokémon Explorer
    </h1>
    <form @submit.prevent="submit">
      <input
        class="block w-150 bg-white/5 h-10 p-4 rounded-full"
        @keyup.enter="submit"
        type="search"
        name=""
        placeholder="Search Pokémon..."
        v-model.trim="text"
      />
    </form>
  </header>

  <section class="buttons flex justify-center items-center flex-wrap gap-4">
    <ButtonComponent
      type="button"
      v-for="(value, key) in typeColors"
      :key="value"
      :id="key"
      :style="{ backgroundColor: value }"
      class="grid px-2 text-white rounded-full border-2 border-[#121212] text-sm cursor-pointer"
      :text="key"
      @click="buttonHandler"
    />
  </section>

  <section
    v-if="gotData"
    class="container flex justify-center items-center flex-wrap gap-4 w-full"
  >
    <PokemonCard
      v-for="pokemon in list"
      :name="pokemon.pokemon.name"
      :url="pokemon.pokemon.url"
      class="grid basis-1/4 gap-4 text-white"
      :key="pokemon.pokemon.name"
      :typeColors
    />
  </section>
  <button
    v-if="gotData"
    type="button"
    @click="loadMore"
    class="grid w-40 p-4 font-bold text-white text-lg rounded-full border-2 bg-white/75 border-[#121212] hover:bg-white hover:text-black active:outline-2 transition duration-300 ease-in-out cursor-pointer justify-self-center"
  >
    Load more
  </button>
</template>
<style scoped>
.active {
  outline: 1px solid white;
}
</style>
