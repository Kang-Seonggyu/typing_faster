<template>
  <header>
    <h1 @click="reloadPage">
      <img
        draggable="false"
        alt="typing_faster logo"
        src="../assets/logo.png"
      />
      <span>typing_faster</span>
    </h1>
    <div class="buttons">
      <MdiIcons :path="'mdiCog'" :button="true" :size="26" />
      <MdiIcons :path="'mdiAlphabeticalVariant'" :button="true" :size="26" />
      <MdiIcons
        v-if="fullscreenFlag"
        :path="'mdiFullscreenExit'"
        :button="true"
        :size="26"
        @click="onFullscreen"
      />
      <MdiIcons
        v-else
        :path="'mdiFullscreen'"
        :button="true"
        :size="26"
        @click="onFullscreen"
      />
    </div>
  </header>
</template>

<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue';
import MdiIcons from '../components/MdiIcons.vue';

const reloadPage = () => {
  window.location.reload();
};

const fullscreenFlag = ref(false);
const onFullscreen = () => {
  if (document.fullscreenElement) {
    document.exitFullscreen();
  } else {
    document.documentElement.requestFullscreen();
  }
  console.log(fullscreenFlag.value);
};

function fullscreenchanged() {
  if (document.fullscreenElement) {
    fullscreenFlag.value = true;
  } else {
    fullscreenFlag.value = false;
  }
}

onMounted(() => {
  document.addEventListener('fullscreenchange', fullscreenchanged);
});

onBeforeUnmount(() => {});
</script>

<style scoped>
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
</style>
