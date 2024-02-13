<template>
  <div class="spelling">
    <span :class="props.typing && props.typing !== props.spell && 'incorrect'">
      {{ props.spell }}
    </span>
  </div>
</template>

<script setup>
const props = defineProps({
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
