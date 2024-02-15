<template>
  <div
    class="container"
    :class="{ open, close: open === false }"
    :style="{ top, left, bottom, right }"
    ref="target"
  >
    <div class="content">
      <div v-if="$slots.header">
        <slot name="header"></slot>
      </div>
      <slot> </slot>
      <div v-if="$slots.footer">
        <slot name="footer"></slot>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onClickOutside } from '@vueuse/core';
import { ref } from 'vue';

const props = defineProps({
  open: { type: Boolean || null, default: false },
  top: { type: String },
  left: { type: String },
  bottom: { type: String },
  right: { type: String },
});
const { top, left, bottom, right } = props;

const emits = defineEmits(['closeMenu']);

const target = ref(null);

onClickOutside(target, (e) => {
  const elName = e.target.nodeName;
  if ((elName === 'svg' || elName === 'path') && props.open) {
    emits('closeMenu', true);
  } else if (props.open) {
    emits('closeMenu', false);
  }
});
</script>

<style scoped>
.container {
  position: absolute;
  z-index: 99;
  overflow: hidden;
  min-width: 120px;
  height: 0;
  background-color: var(--background-color);
  box-shadow: rgba(0, 0, 0, 0.1) 0rem 0.2rem 0.6rem 0rem;
  padding-right: 2px;
}

.content {
  position: relative;
  border: 1px solid #ddd;
  width: 100%;
  height: 100%;
}

.open {
  animation-name: down;
  animation-play-state: running;
  animation-iteration-count: 1;
  animation-direction: normal;
  animation-duration: 0.4s;
  animation-fill-mode: both;
  padding-bottom: 2px;
}
@keyframes down {
  from {
    height: 0%;
  }
  to {
    height: 200px;
  }
}

.close {
  animation-name: up;
  animation-play-state: running;
  animation-iteration-count: 1;
  animation-direction: normal;
  animation-duration: 0.4s;
  animation-fill-mode: both;
}

@keyframes up {
  from {
    height: 200px;
  }
  to {
    height: 0%;
  }
}
</style>
