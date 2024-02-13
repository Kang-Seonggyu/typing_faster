<template>
  <div class="container">
    <header>
      <h1>
        <img
          draggable="false"
          alt="typing_faster logo"
          src="./assets/logo.png"
        />
        <span>typing_faster</span>
      </h1>
      <div class="buttons">
        <MdiIcons :path="'mdiCog'" :button="true" :size="26" />
        <MdiIcons :path="'mdiAlphabeticalVariant'" :button="true" :size="26" />
        <MdiIcons
          :path="'mdiOverscan'"
          :button="true"
          :size="26"
          @click="onFullscreen"
        />
      </div>
    </header>

    <section>
      <TypingBox :msg="randomAdvices" />
    </section>

    <footer>푸터</footer>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import TypingBox from './components/TypingBox.vue';
import { advices } from './api/advices';
import MdiIcons from './components/MdiIcons.vue';

const onFullscreen = () => {
  document.documentElement.requestFullscreen();
};

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
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 15px;
}
header h1 {
  display: inline-flex;
  cursor: pointer;
  align-items: center;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
header h1:active {
  filter: brightness(0.7);
  color: #999;
}
header h1 img {
  width: 70px;
  height: 50px;
}
header h1 span::after {
  content: '⠀';
  display: inline-block;
  margin-left: 4px;
  vertical-align: sub;
  width: 2px;
  height: 30px;
  background-color: rgb(254, 192, 0);
}
header .buttons {
  display: flex;
  gap: 4px;
  margin-right: 10px;
}

section {
  flex: 1;
}
</style>
