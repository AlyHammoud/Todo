<template>
  <div class="full-screen-wrapper">
    <div class="full-screen-text" v-html="contentInFullScreen"></div>
    <p class="close-full-screen" @click="emit('closeFullScreen')">X</p>
  </div>
</template>

<script setup>
import { onMounted } from "@vue/runtime-core";

const { contentInFullScreen } = defineProps({
  contentInFullScreen: {
    type: String,
    default: "",
  },
});

const emit = defineEmits(["closeFullScreen"]);

onMounted(() => {
  document.addEventListener("keydown", (event) => {
    if (event.key === "Escape") {
      emit("closeFullScreen");
    }
  });
});
</script>

<style scoped>
.full-screen-text {
  position: fixed;
  top: 78px;
  left: 0;
  height: calc(100vh - 78px);
  min-height: 100%;
  background: linear-gradient(to right, rgba(0, 0, 55, 0.5), rgb(114, 34, 34));
  backdrop-filter: blur(10px);
  color: white;
  z-index: 999999;
  width: 100%;
  overflow: auto;
  padding: 20px;
  padding-top: 40px;
}

.close-full-screen {
  position: fixed;
  right: 20px;
  top: 45px;
  font-size: 2em;
  z-index: 99999;
  cursor: pointer;
  border: 1px solid #fff;
  border-radius: 50%;
}
</style>