<template>
  <div class="spelling">
    <span>{{ $props.spell }}</span>
    <span>{{ $props.typing }}</span>
  </div>
</template>

<script setup>
defineProps({
  spell: { type: String, required: true },
  typing: { type: String },
});
</script>

<style scoped>
.spelling {
  display: inline-block;
  word-spacing: 10px;
  white-space: pre;
}
span {
  color: #999;
}
</style>
