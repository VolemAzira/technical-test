<script setup>
import { ref, computed } from "vue";
import NotFound from "./pages/NotFound.vue";
import Dashboard from "./pages/Dashboard.vue";
import Overview from "./pages/Overview.vue";

import Sidebar from "./components/Sidebar.vue";
import Header from "./components/Header.vue";

const routes = {
  "/": Dashboard,
  "/overview": Overview,
};

const currentPath = ref(window.location.hash);

window.addEventListener("hashchange", () => {
  currentPath.value = window.location.hash;
});

const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || "/"] || NotFound;
});
</script>

<template>
  <main class="flex">
    <Sidebar />
    <section class="flex-1 h-screen bg-[#F7F8FA]">
      <Header />
      <div class="p-9">
        <component :is="currentView" />
      </div>
    </section>
  </main>
</template>
