<template>
  <div class="container" :class="darkMode && 'dark'">
    <HeaderSection
      @mode-click="darkMode = !darkMode"
      @text-control="updateText"
      :text="text"
    />

    <section>
      <TypingBox :msg="randomAdvices" :text="text" />
    </section>

    <canvas ref="canvas" width="500px" height="340px"></canvas>

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
const text = ref({ color: '#000', size: 16, weight: 400 });

const updateText = (e) => {
  const { name, value } = e;

  text.value[name] = value;
};

const randomAdvices = ref(advices[Math.floor(Math.random() * advices.length)]);

// 아래부터는 canvas
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
