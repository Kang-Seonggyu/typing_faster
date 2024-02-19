<template>
  <label>
    <span class="label">{{ $props.label }}</span>
    <span class="switch">
      <input type="checkbox" @click="toggleCheckbox" />
      <div class="slider round"></div>
    </span>
  </label>
</template>

<script setup>
import { ref } from 'vue';

const checked = ref(false);

defineProps({
  label: { type: String },
});
const emits = defineEmits(['checkboxClick']);

const toggleCheckbox = () => {
  checked.value = !checked.value;
  emits('checkboxClick', checked.value);
};
</script>

<style scoped>
.label {
  margin-right: 2px;
  transition: color 1s ease-in-out;
  color: var(--text-color);
}
.switch {
  position: relative;
  display: inline-block;
  margin-bottom: -2px;
  width: 32px;
  height: 16px;
}

.switch input {
  display: none;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

.slider:before {
  position: absolute;
  content: '';
  height: 10px;
  width: 10px;
  left: 3px;
  bottom: 3px;
  background-color: white;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

input:checked + .slider {
  background-color: #66abcc;
}

input:focus + .slider {
  box-shadow: 0 0 1px #66abcc;
}

input:checked + .slider:before {
  -webkit-transform: translateX(16px);
  -ms-transform: translateX(16px);
  transform: translateX(16px);
}

.slider.round {
  border-radius: 16px;
}

.slider.round:before {
  border-radius: 50%;
}
</style>
