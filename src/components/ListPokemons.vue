<script setup>
const pokemon = defineProps([
  "name",
  "urlBaseSvg"
]);
</script>

<template>
  <article
    class="
      group
      cursor-pointer
      rounded-3xl
      border
      border-white/8
      bg-[#151A46]/85
      p-4
      sm:p-5
      w-full
      min-w-0
      overflow-hidden
      transition-all
      duration-300
      hover:-translate-y-2
      hover:border-violet-400/40
      hover:bg-[#1A2052]
      hover:shadow-[0_20px_45px_rgba(124,92,255,.18)]
    "
  >

    <!-- Imagem -->

    <div
      class="
        flex
        h-28
        items-center
        justify-center
      "
    >

      <img
        :src="urlBaseSvg"
        :alt="pokemon.name"
        loading="lazy"
        class="
          h-20
          w-auto
          max-w-full
          transition-all
          duration-300
          group-hover:scale-110
          group-hover:drop-shadow-[0_0_18px_rgba(124,92,255,.55)]
        "
      />

    </div>

    <!-- Nome -->

    <div class="mt-5 w-full text-center">

      <h3
        class="
          w-full
          min-w-0
          max-w-full
          text-center
          font-semibold
          capitalize
          text-white
          text-[15px]
          sm:text-base
          break-words
          leading-snug
          line-clamp-2
        "
      >
        {{ pokemon.name }}
      </h3>

      <span
        class="
          mt-2
          inline-flex
          rounded-full
          bg-white/5
          px-3
          py-1
          text-[11px]
          tracking-widest
          uppercase
          text-slate-400
          max-w-full
        "
      >
        Pokémon
      </span>

    </div>

  </article>
</template>

<style scoped>

@media (min-width: 1024px) {
  article {
    backdrop-filter: blur(18px);
  }
}

</style>