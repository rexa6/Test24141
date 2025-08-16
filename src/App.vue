<script setup>
import { ref } from "vue";
import BottomNav from "./components/BottomNav.vue";

// Импортируем страницы
import Upgrade from "./components/Upgrade.vue";
import Flip from "./components/Flip.vue";
import Minki from "./components/Minki.vue";
import Profile from "./components/Profile.vue";

const activeTab = ref("Upgrade");

const componentsMap = {
  Upgrade,
  Flip,
  Minki,
  Profile
};
</script>

<template>
  <div class="app">
    <!-- Контент -->
    <component :is="componentsMap[activeTab]" />

    <!-- Нижний таб-бар -->
    <BottomNav v-model:activeTab="activeTab" />
  </div>
</template>

<style>
.app {
  min-height: 100vh;
  background: linear-gradient(135deg, #1a0d2e 0%, #2a1a4d 100%);
  color: #fff;
  padding-bottom: 120px; /* чтобы таб-бар не перекрывал контент */
}
</style>
