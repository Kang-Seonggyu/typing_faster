<template>
  <footer>
    <div class="circle" style="background: #3b87aa">
      <MdiIcons path="mdiCoffee" :size="25" />
    </div>
    <div class="circle" style="background: #633a18">
      <MdiIcons path="mdiFileDocumentEditOutline" :size="25" />
    </div>
  </footer>
</template>

<script setup>
import MdiIcons from '../components/common/MdiIcons.vue';
</script>

<style scoped>
footer {
  position: fixed;
  display: flex;
  gap: 10px;
  right: 40px;
  bottom: 30px;
}
.circle {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 50px;
  height: 50px;
  color: white;
  border-radius: 50%;
  transition: scale 200ms ease-in-out;
  box-shadow: rgba(0, 0, 0, 0.15) 0px 4px 8px;
}
.circle:hover {
  cursor: pointer;
  scale: 1.1;
}
</style>
