<template>
  <input
    type="range"
    :max="props.max"
    :min="props.min"
    :step="props.step"
    v-model="value"
    @input="updateSlider"
    :style="{ backgroundSize: backgroundSize, width: props.width }"
  />
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
  width: { type: String },
  value: { type: Number, default: 20 },
  min: { type: Number, default: 0 },
  max: { type: Number, default: 100 },
  step: { type: Number, default: 1 },
});

const value = ref(props.value);
const backgroundSize = ref(`${props.value}% 100%`);

const updateSlider = (e) => {
  let clickedElement = e.target,
    min = clickedElement.min,
    max = clickedElement.max,
    val = clickedElement.value;

  backgroundSize.value = ((val - min) * 100) / (max - min) + '% 100%';
};
</script>

<style scoped>
input[type='range'] {
  -webkit-appearance: none;
  display: block;
  width: 100%;
  margin: 10px auto;
  background: #3e3e3f;
  background-image: -webkit-gradient(linear, 20% 0%, 20% 100%);
  background-image: -webkit-linear-gradient(left, #add8e6 0%, #add8e6 100%);
  background-image: -moz-linear-gradient(left, #add8e6 0%, #add8e6 100%);
  background-image: -o-linear-gradient(to right, #add8e6 0%, #add8e6 100%);
  background-image: linear-gradient(to right, #add8e6 0%, #add8e6 100%);
  background-repeat: no-repeat;
}
input[type='range']:focus {
  outline: none;
}
input[type='range']::-webkit-slider-runnable-track {
  width: 100%;
  height: 4px;
  cursor: pointer;
  box-shadow: none;
  background: transparent;
  border-radius: 0px;
  border: none;
}
input[type='range']::-webkit-slider-thumb {
  box-shadow: none;
  border: 4px solid #add8e6;
  height: 16px;
  width: 16px;
  border-radius: 2px;
  background: #3e3e3f;
  cursor: pointer;
  -webkit-appearance: none;
  margin-top: -6px;
}
input[type='range']:focus::-webkit-slider-runnable-track {
  background: transparent;
}
input[type='range']::-moz-range-track {
  width: 100%;
  height: 4px;
  cursor: pointer;
  box-shadow: none;
  background: transparent;
  border-radius: 0px;
  border: none;
}
input[type='range']::-moz-range-thumb {
  box-shadow: none;
  border: 4px solid #add8e6;
  height: 16px;
  width: 16px;
  border-radius: 2px;
  background: #ffffff;
  cursor: pointer;
}
input[type='range']::-ms-track {
  width: 100%;
  height: 4px;
  cursor: pointer;
  background: transparent;
  border-color: transparent;
  color: transparent;
}
input[type='range']::-ms-fill-lower {
  background: transparent;
  border: none;
  border-radius: 0px;
  box-shadow: none;
}
input[type='range']::-ms-fill-upper {
  background: transparent;
  border: none;
  border-radius: 0px;
  box-shadow: none;
}
input[type='range']::-ms-thumb {
  box-shadow: none;
  border: 4px solid #add8e6;
  height: 16px;
  width: 16px;
  border-radius: 2px;
  background: #ffffff;
  cursor: pointer;
  height: 4px;
}
input[type='range']:focus::-ms-fill-lower {
  background: transparent;
}
input[type='range']:focus::-ms-fill-upper {
  background: transparent;
}
</style>
