<template>
  <div class="container">
    <HeaderSection />

    <section>
      <TypingBox :msg="randomAdvices" />
    </section>

    <FooterSection />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import TypingBox from './components/TypingBox.vue';
import { advices } from './api/advices';

import FooterSection from './layouts/FooterSection.vue';
import HeaderSection from './layouts/HeaderSection.vue';

const randomAdvices = ref(advices[Math.floor(Math.random() * advices.length)]);
</script>

<style scoped>
.container {
  min-width: 500px;
  min-height: 500px;
  height: 100vh;
  display: flex;
  flex-direction: column;
}

section {
  flex: 1;
}
</style>
