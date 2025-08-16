<script setup>
import { ref, computed, nextTick } from "vue";

const activeTab = ref("Upgrade");
const tabs = [
  { name: "Upgrade", icon: "⚡" },
  { name: "Flip", icon: "🔥" },
  { name: "Minki", icon: "🚀" },
  { name: "Profile", icon: "👤" }
];

const tabWidths = ref([]);
const tabOffsets = ref([]);

function setTab(tabName) {
  activeTab.value = tabName;
  nextTick(() => updateIndicator());
}

function updateIndicator() {
  const liElements = document.querySelectorAll(".nav li");
  tabWidths.value = Array.from(liElements).map(el => el.offsetWidth);
  tabOffsets.value = Array.from(liElements).map(el => el.offsetLeft);
}

window.addEventListener("resize", updateIndicator);
</script>

<template>
  <div class="app">
    <div class="content">
      <div class="hero">
        <h1 class="hero-title">Добро пожаловать!</h1>
        <p class="hero-subtitle">Выбранная вкладка: <strong>{{ activeTab }}</strong></p>
      </div>
    </div>

    <nav class="nav">
      <ul>
        <li
          v-for="tab in tabs"
          :key="tab.name"
          @click="setTab(tab.name)"
          :class="{ active: tab.name === activeTab }"
        >
          <span class="icon">{{ tab.icon }}</span>
          <span class="label">{{ tab.name }}</span>
        </li>
      </ul>
      <div
        class="indicator"
        :style="{
          width: tabWidths[tabs.findIndex(t => t.name === activeTab)] + 'px',
          left: tabOffsets[tabs.findIndex(t => t.name === activeTab)] + 'px'
        }"
      ></div>
    </nav>
  </div>
</template>

<style scoped>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

.app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  background: linear-gradient(135deg, #1a0d2e 0%, #2a1a4d 100%);
  color: #fff;
  position: relative;
  overflow: hidden;
}

.app::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: radial-gradient(circle at 50% 50%, rgba(255, 255, 255, 0.1) 0%, transparent 70%);
  pointer-events: none;
}

.content {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
  position: relative;
  z-index: 1;
}

.hero {
  text-align: center;
  animation: fadeIn 1s ease-out;
}

.hero-title {
  font-size: 3rem;
  font-weight: 800;
  background: linear-gradient(45deg, #f107a3, #00ddeb);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
  margin-bottom: 1rem;
  text-shadow: 0 0 20px rgba(241, 7, 163, 0.5);
}

.hero-subtitle {
  font-size: 1.5rem;
  color: #ddd;
  letter-spacing: 1px;
}

.nav {
  position: fixed;
  bottom: 20px;
  left: 20px;
  right: 20px;
  background: rgba(42, 26, 77, 0.9);
  backdrop-filter: blur(10px);
  border-radius: 20px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
  padding: 10px;
  z-index: 2;
}

.nav ul {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
}

.nav li {
  flex: 1;
  text-align: center;
  padding: 12px 0;
  cursor: pointer;
  display: flex;
  flex-direction: column;
  align-items: center;
  transition: transform 0.3s ease, color 0.3s ease;
}

.nav li:hover {
  transform: translateY(-4px);
}

.nav li.active {
  color: #f107a3;
  transform: scale(1.1);
}

.nav .icon {
  font-size: 24px;
  margin-bottom: 6px;
  transition: transform 0.3s ease;
}

.nav li:hover .icon {
  transform: scale(1.2);
}

.nav .label {
  font-size: 12px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.indicator {
  position: absolute;
  bottom: 0;
  height: 4px;
  background: linear-gradient(90deg, #f107a3, #00ddeb);
  border-radius: 2px;
  transition: all 0.3s cubic-bezier(0.68, -0.55, 0.265, 1.55);
  box-shadow: 0 0 15px rgba(241, 7, 163, 0.7);
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}

@media (max-width: 600px) {
  .hero-title {
    font-size: 2rem;
  }
  .hero-subtitle {
    font-size: 1.2rem;
  }
  .nav {
    bottom: 10px;
    left: 10px;
    right: 10px;
  }
  .nav .icon {
    font-size: 20px;
  }
  .nav .label {
    font-size: 10px;
  }
}
</style>