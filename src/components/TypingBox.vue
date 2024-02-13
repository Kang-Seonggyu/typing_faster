<template>
  <!-- <div class="custom-caret" ref="caret"></div> -->
  <div class="dictation">
    <div
      class="typing__container"
      @input="onTyping"
      @keydown="onKeydown"
      ref="editableDiv"
      contenteditable="true"
    ></div>
    <div class="dictation__label">
      <OneSpelling
        v-for="(spell, idx) in msg.replace(/&nbsp;/g, ' ')"
        :key="`spell_${idx}`"
        :spell="spell"
        :typing="typingText[idx]"
      />
    </div>
    <div class="speed">
      <em style="color: rgb(118, 103, 238)">WPM</em>
      <p>{{ calculateTypingSpeed(startTime, endTime)[0] || '0' }}</p>
      <em style="color: rgb(0, 211, 175)">CPM</em>
      <p>{{ calculateTypingSpeed(startTime, endTime)[1] || '0' }}</p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, computed } from 'vue';
import OneSpelling from './OneSpelling.vue';

const props = defineProps({
  msg: { type: String, required: true },
});

const editableDiv = ref(null);
const startTime = ref(0);
const endTime = ref(0);
const typingText = ref('');
const errorMsg = ref('');
const typingCount = ref(0);

const onTyping = (e) => {
  if (!startTime.value) {
    startTime.value = Date.now();
  }
  typingText.value = e.target.innerHTML.replace(/&nbsp;/g, ' ');
  // moveCaret();
};

const onKeydown = (e) => {
  const keyCode = e.keyCode || e.which;

  if (e.code === 'Backspace') {
    if (typingCount.value === 0) {
      typingCount.value = 0;
    } else {
      typingCount.value -= 1;
    }
  } else if (e.code.includes('Enter')) {
    e.preventDefault();
    if (typingText.value === props.msg) {
      errorMsg.value = '';
      endTime.value = Date.now();
    } else {
      errorMsg.value = '오타가 있습니다. 확인해주세요.';
    }
  } else if (
    (keyCode >= 65 && keyCode <= 90) || // A-Z
    (keyCode >= 97 && keyCode <= 122) || // a-z
    (keyCode >= 48 && keyCode <= 57) || // 0-9
    keyCode === 188 || // ',' : comma
    keyCode === 190 || // '.' : period
    keyCode === 229
  ) {
    typingCount.value += 1;
  } else {
    return;
  }
};

const calculateTypingSpeed = (start, end) => {
  if (start === 0 && end === 0) {
    return 0;
  }
  const elapsedSeconds = (end - start) / 1000;
  const typingwordSpeed =
    Math.round((typingText.value.length / elapsedSeconds) * 16) || 0;
  const typingSpeed =
    Math.round((typingCount.value / elapsedSeconds) * 60) || 0;
  return [typingwordSpeed, typingSpeed];
};

// const caret = ref(null);

// const moveCaret = () => {
//   const selection = window.getSelection();
//   const range = selection.getRangeAt(0);
//   const rect = range.getBoundingClientRect();

//   console.log('렉트:', rect);

//   caret.value.style.top = `${rect.top}px`;
//   caret.value.style.left = `${rect.left}px`;
//   caret.value.style.height = `${rect.height}px`;
// };

onMounted(() => {
  editableDiv.value.focus();
  // moveCaret();
});
onUnmounted(() => {
  editableDiv.value.removeEventListener('input', handleInput);
});
</script>

<style scoped>
.dictation {
  position: relative;
  overflow: hidden;
  box-sizing: border-box;
  width: 100%;
  min-height: 200px;
  padding: 20px 60px 20px 100px;
}
.typing__container {
  position: absolute;
  box-sizing: border-box;
  word-break: break-all;
  top: 20px;
  left: 100px;
  right: 60px;
  bottom: 20px;
  z-index: 10;
  caret-color: rgb(254, 192, 0);
}
.typing__container:focus {
  outline: none;
}
@keyframes blink-effect {
  50% {
    opacity: 0;
  }
}
.custom-caret {
  position: absolute;
  height: 1.3em;
  width: 2px;
  background-color: rgb(254, 192, 0);
  animation: blink-effect infinite step-end 1s;
}
.speed {
  position: absolute;
  left: 40px;
  top: 20px;
  padding: 4px;
  text-align: center;
  border: 1px solid #ccc;
  border-radius: 8px;
}
.speed em {
  font-style: normal;

  font-size: 14px;
  font-weight: bold;
}
.speed p {
  margin: 0;
}
/* .dictation__label {
} */
</style>
