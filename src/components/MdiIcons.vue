<template>
  <div
    :class="[props.button && 'button', props.tooltip && 'tooltip']"
    :data-tooltip="props.tooltip"
  >
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
  tooltip: { type: String, default: '' },
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
  position: relative;
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

.tooltip::before {
  visibility: hidden;
  position: absolute;
  top: 40px;
  left: 50%;
  margin-left: -40px;
  display: inline-block;
  width: 70px;
  padding: 2px 6px;
  text-align: center;
  z-index: 10;
  font-size: 14px;
  content: attr(data-tooltip);
  color: var(--background-color);
  background-color: var(--text-color);
  border-radius: 4px;
}
.tooltip::after {
  visibility: hidden;
  content: '';
  position: absolute;
  display: inline-block;
  top: 26px;
  left: 50%;
  width: 1px;
  margin-top: 2px;
  margin-left: -5px;
  border: 6px solid transparent;
  border-bottom-color: var(--text-color);
}
.tooltip:hover::before,
.tooltip:hover::after {
  visibility: visible;
}
</style>
<style>
.button svg path {
  fill: #666;
}
</style>
