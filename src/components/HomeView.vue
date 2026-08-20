<script setup>
import { onMounted, ref, computed } from "vue";

import ListPokemons from "./ListPokemons.vue";
import CardPokemonSelected from "./CardPokemonSelected.vue";

const urlBaseSvg = ref(
  "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/"
);

const pokemons = ref([]);
const pokemonSelected = ref(null);
const searchPokemonField = ref("");
const loading = ref(false);

onMounted(() => {
  fetch("https://pokeapi.co/api/v2/pokemon?limit=1302&offset=0")
    .then((res) => res.json())
    .then((res) => {
      pokemons.value = res.results;
    });
});

const pokemonsFiltered = computed(() => {
  if (!pokemons.value.length) return [];

  if (searchPokemonField.value.trim()) {
    return pokemons.value.filter((pokemon) =>
      pokemon.name
        .toLowerCase()
        .includes(searchPokemonField.value.toLowerCase())
    );
  }

  return pokemons.value.slice(0, 30);
});

const selectPokemon = async (pokemon) => {
  loading.value = true;

  try {
    const response = await fetch(pokemon.url);
    pokemonSelected.value = await response.json();
  } catch (error) {
    console.error(error);
  } finally {
    loading.value = false;
  }
};
</script>

<template>
  <main class="relative overflow-x-hidden py-3">
    <!-- Glow Background -->
    <div
      class="absolute -left-20 -top-36 h-[300px] w-[300px] rounded-full bg-violet-600/15 blur-[180px] md:-left-52 md:-top-72 md:h-[550px] md:w-[550px]"
    ></div>

    <div
      class="absolute bottom-0 right-0 h-[300px] w-[300px] rounded-full bg-cyan-500/10 blur-[180px] md:h-[500px] md:w-[500px]"
    ></div>

    <div
      class="relative z-10 mx-auto w-full max-w-[1200px] px-5"
    >
      <div
        class="grid gap-6 xl:grid-cols-[280px_minmax(0,1fr)] 2xl:grid-cols-[330px_minmax(0,1fr)]"
      >
        <!-- CARD ESQUERDO -->
        <CardPokemonSelected
          :name="pokemonSelected?.name"
          :xp="pokemonSelected?.base_experience"
          :height="pokemonSelected?.height"
          :img="pokemonSelected?.sprites?.other?.dream_world?.front_default"
          :loading="loading"
        />

        <!-- LISTA -->
        <section
          class="overflow-visible rounded-[28px] border border-white/10 bg-white/5 shadow-[0_25px_70px_rgba(0,0,0,.35)] md:backdrop-blur-2xl pb-2"
        >
          <div class="p-4 md:p-6">
            <!-- HEADER -->
            <div
              class="mb-2 flex flex-col xl:flex-row xl:items-center xl:justify-between"
            >
              <div>
                <h1 class="text-4xl font-bold text-white xl:text-5xl">
                  Pokedex
                </h1>

                <p class="mt-1 text-slate-400">
                  Escolha um Pokemon para visualizar seus detalhes.
                </p>
              </div>

              <!-- SEARCH -->
              <div class="relative w-full xl:w-[340px]">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke-width="2"
                  stroke="currentColor"
                  class="absolute left-5 top-1/2 h-5 w-5 -translate-y-1/2 text-slate-500"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    d="m21 21-4.35-4.35M16.65 10.825a5.825 5.825 0 1 1-11.65 0 5.825 5.825 0 0 1 11.65 0Z"
                  />
                </svg>

                <input
                  v-model="searchPokemonField"
                  type="text"
                  placeholder="Pesquisar Pokemon..."
                  class="w-full rounded-2xl border border-white/10 bg-[#181D4A] py-3 pl-14 pr-5 text-white outline-none transition-all placeholder:text-slate-500 focus:border-violet-500 focus:ring-4 focus:ring-violet-500/20"
                />
              </div>
            </div>

            <!-- GRID -->
            <div class="card-list-wrapper mt-6">
              <div class="card-list pt-10 grid">
                <ListPokemons
                  v-for="pokemon in pokemonsFiltered"
                  :key="pokemon.name"
                  :name="pokemon.name"
                  :urlBaseSvg="urlBaseSvg + pokemon.url.split('/')[6] + '.svg'"
                  @click="selectPokemon(pokemon)"
                />
              </div>
            </div>
          </div>
        </section>
      </div>
    </div>
  </main>
</template>

  <style scoped>
  .card-list-wrapper {
    max-height: 72vh;
    overflow-y: auto;
    overflow-x: hidden;
    overscroll-behavior: contain;
    padding-right: 6px;

    scrollbar-width: thin;
    scrollbar-color: rgba(124, 92, 255, 0.45) transparent;
  }

  .card-list {
    display: grid;
    gap: 1.25rem;
    grid-template-columns: repeat(2, minmax(140px, 1fr));
  }

  .card-list::-webkit-scrollbar {
    width: 8px;
  }

  .card-list::-webkit-scrollbar-track {
    background: transparent;
  }

  .card-list::-webkit-scrollbar-thumb {
    background: rgba(124, 92, 255, 0.35);
    border-radius: 999px;
  }

  .card-list::-webkit-scrollbar-thumb:hover {
    background: rgba(124, 92, 255, 0.65);
  }

  @media (max-width: 374px) {
    .card-list {
      grid-template-columns: 1fr;
      gap: 0.75rem;
    }
  }

  @media (min-width: 400px) {
    .card-list {
      grid-template-columns: repeat(2, minmax(150px, 1fr));
    }
  }

  @media (min-width: 640px) {
    .card-list {
      grid-template-columns: repeat(3, minmax(150px, 1fr));
    }
  }

  @media (min-width: 768px) {
    .card-list {
      grid-template-columns: repeat(3, minmax(160px, 1fr));
    }
  }

  @media (min-width: 1024px) {
    .card-list {
      grid-template-columns: repeat(4, minmax(160px, 1fr));
    }
  }

  @media (min-width: 1280px) {
    .card-list {
      grid-template-columns: repeat(5, minmax(160px, 1fr));
    }
  }
  </style>













