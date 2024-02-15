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
      <MdiIcons
        :path="'mdiCog'"
        :button="true"
        :size="26"
        tooltip="기본설정"
        @click="
          () => {
            abcSettingOpen = false;
            basicSettingOpen = !basicSettingOpen;
          }
        "
      />
      <SettingMenu
        :open="basicSettingOpen"
        top="64px"
        right="70px"
        @close-menu="(e) => (basicSettingOpen = e)"
      >
        <template #header>
          <div>설정</div>
        </template>
        <template #default>
          <ToggleSwitch @checkbox-click="$emit('modeClick')" label="다크모드" />
        </template>
      </SettingMenu>
      <MdiIcons
        :path="'mdiAlphabeticalVariant'"
        :button="true"
        :size="26"
        tooltip="언어설정"
        @click="
          () => {
            basicSettingOpen = false;
            abcSettingOpen = !abcSettingOpen;
          }
        "
      />
      <SettingMenu
        :open="abcSettingOpen"
        top="64px"
        right="30px"
        @close-menu="(e) => (abcSettingOpen = e)"
      >
        <template #header> 언어설정 </template>
        <template #default>
          <div>
            <label>Color</label>
          </div>
          <div>
            <label>Weight</label>
          </div>
          <div>
            <label>Size</label>
          </div>
        </template>
      </SettingMenu>
      <MdiIcons
        v-if="fullscreenFlag"
        :path="'mdiFullscreenExit'"
        :button="true"
        :size="26"
        @click="onFullscreen"
        tooltip="화면축소"
      />
      <MdiIcons
        v-else
        :path="'mdiFullscreen'"
        :button="true"
        :size="26"
        @click="onFullscreen"
        tooltip="화면확대"
      />
    </div>
  </header>
</template>

<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue';
import MdiIcons from '../components/common/MdiIcons.vue';
import SettingMenu from '../components/SettingMenu.vue';
import ToggleSwitch from '../components/common/ToggleSwitch.vue';

const reloadPage = () => {
  window.location.reload();
};

defineEmits(['modeClick']);

const basicSettingOpen = ref(null);
const abcSettingOpen = ref(null);

const fullscreenFlag = ref(false);
const onFullscreen = () => {
  if (document.fullscreenElement) {
    document.exitFullscreen();
  } else {
    document.documentElement.requestFullscreen();
  }
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

onBeforeUnmount(() => {
  document.removeEventListener('fullscreenchange');
});
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
