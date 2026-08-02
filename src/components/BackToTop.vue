<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const showButton = ref(false);

const handleScroll = () => {
  showButton.value = window.scrollY > 350;
};

const scrollTop = () => {
  window.scrollTo({
    top: 0,
    behavior: "smooth",
  });
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
});
</script>

<template>
  <Transition name="fade">
    <button
      v-if="showButton"
      @click="scrollTop"
      class="
      fixed
      bottom-4
      right-4
      z-50

      flex
      h-12
      w-12
      items-center
      justify-center

      rounded-2xl

      border
      border-white/10

      bg-[#171B4B]/90

      sm:backdrop-blur-xl

      text-white

      shadow-[0_15px_40px_rgba(124,92,255,.35)]

      transition-all
      duration-300

      hover:-translate-y-1
      hover:scale-105
      hover:border-violet-400
      hover:shadow-[0_20px_55px_rgba(124,92,255,.55)]
      sm:bottom-8 sm:right-8 sm:h-14 sm:w-14
      "
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-6 w-6"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
        stroke-width="2.3"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          d="M5 15l7-7 7 7"
        />
      </svg>
    </button>
  </Transition>
</template>

<style scoped>

.fade-enter-active,
.fade-leave-active{
transition:all .25s ease;
}

.fade-enter-from,
.fade-leave-to{
opacity:0;
transform:translateY(20px);
}

</style>