<script setup>
import { ref, nextTick, onMounted } from "vue";

const props = defineProps({
  activeTab: String
});
const emit = defineEmits(["update:activeTab"]);

const tabs = [
  { name: "Upgrade", icon: "⚡" },
  { name: "Flip", icon: "🔥" },
  { name: "Minki", icon: "🚀" },
  { name: "Profile", icon: "👤" }
];

const tabWidths = ref([]);
const tabOffsets = ref([]);

function setTab(tabName) {
  emit("update:activeTab", tabName);
  nextTick(() => updateIndicator());
}

function updateIndicator() {
  const liElements = document.querySelectorAll(".nav li");
  tabWidths.value = Array.from(liElements).map(el => el.offsetWidth);
  tabOffsets.value = Array.from(liElements).map(el => el.offsetLeft);
}

onMounted(() => {
  updateIndicator();
  window.addEventListener("resize", updateIndicator);
});
</script>

<template>
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
        width: tabWidths[tabs.findIndex(t => t.name === activeTab)] - 12 + 'px',
        left: tabOffsets[tabs.findIndex(t => t.name === activeTab)] + 6 + 'px'
      }"
    ></div>
  </nav>
</template>

<style scoped>
.nav {
  position: fixed;
  bottom: 40px;
  left: 25px;
  right: 25px;
  background: rgba(42, 26, 77, 0.9);
  backdrop-filter: blur(10px);
  border-radius: 20px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
  padding: 10px 0;
  z-index: 10;
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
  top: 0;
  height: 4px;
  background: linear-gradient(90deg, #f107a3, #00ddeb);
  border-radius: 2px;
  transition: all 0.3s cubic-bezier(0.68, -0.55, 0.265, 1.55);
  box-shadow: 0 0 15px rgba(241, 7, 163, 0.7);
}
</style>
