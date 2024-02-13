<template>
  <div :class="props.button && 'button'">
    <SvgIcon class="mdiIcon" v-if="icon" type="mdi" :path="icon" :size="size" />
  </div>
</template>

<script setup>
import SvgIcon from '@jamescoyle/vue-icon';
import { onMounted, ref } from 'vue';

const props = defineProps({
  path: { type: String, required: true },
  size: { type: Number, default: 24 },
  button: { type: Boolean, default: false },
});

const icon = ref(null);

onMounted(() => {
  import('@mdi/js')
    .then((module) => {
      icon.value = module[props.path];
    })
    .catch((error) => {
      console.error(`Failed to load icon: ${error}`);
    });
});
</script>

<style scoped>
.button {
  display: flex;
  padding: 2px 4px;
  border: 1px solid #ddd;
  border-radius: 5px;
  box-shadow: rgba(0, 0, 0, 0.1) 0rem 0.2rem 0.6rem 0rem;
}
.button:hover {
  cursor: pointer;
  background-color: #ddd;
}
</style>
<style>
.button svg path {
  fill: #666;
}
</style>
