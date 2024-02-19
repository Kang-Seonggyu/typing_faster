<template>
  <div class="spelling">
    <span
      :class="props.typing && props.typing !== props.spell && 'incorrect'"
      :style="{
        fontSize: props.text?.size + 'px',
        fontWeight: props.text?.weight,
      }"
    >
      {{ props.spell }}
    </span>
  </div>
</template>

<script setup>
import { watch } from 'vue';

const props = defineProps({
  text: { type: Object },
  spell: { type: String, required: true },
  typing: { type: String },
});
</script>

<style scoped>
.spelling {
  display: inline-block;
  white-space: pre;
}
span {
  color: #999;
}
span.incorrect {
  position: relative;
  z-index: 10;
  color: rgba(255, 0, 0, 0.7);
  font-weight: bold;
}
</style>
