<template>
  <!-- <div class="custom-caret" ref="caret"></div> -->
  <div class="dictation">
    <div
      class="typing__container"
      @input="onTyping"
      ref="editable"
      contenteditable="true"
    ></div>
    <div class="dictation__label">
      <OneSpelling
        v-for="(spell, idx) in msg"
        :key="`spell_${idx}`"
        :spell="spell"
      />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import OneSpelling from './OneSpelling.vue';

const props = defineProps({
  msg: { type: String, required: true },
});

const editable = ref(null);
const typingText = ref('');
const onTyping = (e) => {
  typingText.value = e.target.innerHTML;
  // moveCaret();
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
  editable.value.focus();
  // moveCaret();
});
onUnmounted(() => {
  editable.value.removeEventListener('input', handleInput);
});
</script>

<style scoped>
.dictation {
  position: relative;
  overflow: hidden;
  box-sizing: border-box;
  width: 100%;
  padding: 20px 60px;
}
.typing__container {
  position: absolute;
  box-sizing: border-box;
  word-break: break-all;
  top: 20px;
  left: 60px;
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
/* .dictation__label {
} */
</style>
