<template>
  <div class="container" :class="darkMode && 'dark'">
    <HeaderSection @mode-click="darkMode = !darkMode" />

    <section>
      <TypingBox :msg="randomAdvices" />
    </section>

    <FooterSection />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { advices } from './api/advices';

import HeaderSection from './layouts/HeaderSection.vue';
import FooterSection from './layouts/FooterSection.vue';
import TypingBox from './components/TypingBox.vue';

const darkMode = ref(false);

const randomAdvices = ref(advices[Math.floor(Math.random() * advices.length)]);
</script>

<style scoped>
:root {
  --background: blue;
}
.container {
  min-width: 500px;
  min-height: 500px;
  height: 100vh;
  display: flex;
  flex-direction: column;
  color: var(--text-color);
  background-color: var(--background-color);
  transition-property: color, background-color;
  transition-duration: 1s;
  transition-timing-function: ease-in-out;
}

section {
  flex: 1;
}
</style>
