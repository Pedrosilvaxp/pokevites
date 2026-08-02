<script setup>
const pokemon = defineProps([
  "name",
  "xp",
  "height",
  "img",
  "loading",
]);
</script>

<template>
  <aside
    class="relative overflow-hidden rounded-[32px] border border-white/10 bg-white/5 backdrop-blur-2xl shadow-[0_20px_60px_rgba(0,0,0,.45)]"
  >

    <!-- Glow -->

    <div
      class="absolute left-1/2 top-32 h-48 w-48 -translate-x-1/2 rounded-full bg-violet-600/25 blur-[110px]"
    ></div>

    <div class="relative z-10 p-6">

      <!-- Badge -->

      <div
        class="mb-6 inline-flex rounded-full border border-violet-500/20 bg-violet-500/10 px-4 py-2 text-xs font-semibold uppercase tracking-[.25em] text-violet-300"
      >
        Pokémon Selecionado
      </div>

      <!-- Imagem -->

      <div
        class="flex h-[240px] items-center justify-center"
      >

        <img
          v-if="pokemon.name"
          :src="pokemon.img"
          :alt="pokemon.name"
          class="h-60 w-auto drop-shadow-[0_25px_45px_rgba(124,92,255,.45)] transition-all duration-500 hover:scale-105 will-change-transform"
        />

        <img
          v-else
          src="../assets/egg_pokemon.svg"
          alt="egg"
          class="egg h-60 w-auto opacity-90"
        />

      </div>

      <!-- Nome -->

      <div class="mt-3 text-center">

        <h2
          class="text-3xl font-bold capitalize tracking-wide text-white"
        >
          {{ pokemon.name || "Unknown Pokémon" }}
        </h2>

        <p
          class="mt-2 text-sm text-slate-400"
        >
          Escolha um Pokémon para visualizar seus dados.
        </p>

      </div>

      <!-- Informações -->

      <div class="mt-10 grid grid-cols-2 gap-4">

        <div
          class="rounded-2xl border border-white/10 bg-[#171B4B] p-2 text-sm"
        >
          <span
            class="uppercase tracking-widest text-slate-500"
          >
            Base XP
          </span>

          <h3
            class="mt-2 text-sm font-bold text-white"
          >
            {{ pokemon.xp || "??" }}
          </h3>
        </div>

        <div
          class="rounded-2xl border border-white/10 bg-[#171B4B] p-2 text-sm"
        >
          <span
            class="uppercase tracking-widest text-slate-500"
          >
            Altura
          </span>

          <h3
            class="mt-2 text-sm font-bold text-white"
          >
            {{ pokemon.height || "??" }}
          </h3>
        </div>

      </div>

    </div>
  </aside>
</template>

<style scoped>

.egg{

animation:float 3.8s ease-in-out infinite;

filter:drop-shadow(0 0 45px rgba(124,92,255,.45));

will-change:transform;

}

@keyframes float{

0%{

transform:translateY(0px);

}

50%{

transform:translateY(-14px);

}

100%{

transform:translateY(0px);

}

}

@media(min-width:1280px){

aside{

position:sticky;

top:0.5rem;

}

}

</style>

