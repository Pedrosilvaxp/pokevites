<script setup>
import HomeView from "./components/HomeView.vue";
import BackToTop from "./components/BackToTop.vue";

</script>

<template>
  <div
    class="
      min-h-dvh
      flex
      flex-col
      bg-[#0C0D38]
      overflow-x-hidden
    "
  >
    <!-- Background Glow -->

    <div
      class="fixed inset-0 -z-10 overflow-hidden"
    >
      <div
        class="absolute -left-48 -top-48 h-[520px] w-[520px] rounded-full bg-violet-600/15 blur-[180px]"
      />

      <div
        class="absolute right-[-120px] top-1/3 h-[420px] w-[420px] rounded-full bg-cyan-400/10 blur-[170px]"
      />

      <div
        class="absolute bottom-[-200px] left-1/2 h-[500px] w-[500px] -translate-x-1/2 rounded-full bg-blue-500/10 blur-[200px]"
      />
    </div>

    <!-- Conteúdo -->

    <main class="flex-1">
      <HomeView />
    </main>

    <BackToTop />

    <!-- Footer -->

    <footer
      class="
        border-t
        border-white/10

        bg-[#131742]/80
        backdrop-blur-xl

        py-4

        text-center
        text-sm
        text-slate-400
      "
    >
      © {{ new Date().getFullYear() }}

      <span class="mx-2 text-violet-400">
        •
      </span>

      <span class="font-semibold text-white">
        PokeVite
      </span>

      <span class="mx-2 text-violet-400">
        •
      </span>

      Desenvolvido com Vue + Tailwind
    </footer>
  </div>
</template>

<style>
@import "tailwindcss";

html,
body,
#app {

  margin: 0;
  padding: 0;

  width: 100%;
  min-height: 100dvh;

  overflow-x: hidden;

  background: #0C0D38;

}

body{

  font-family:
  Inter,
  system-ui,
  -apple-system,
  BlinkMacSystemFont,
  "Segoe UI",
  sans-serif;

}
</style>