<template>
  <div class="relative w-full h-screen flex justify-center items-center bg-black overflow-hidden" @mousemove="handleMouseMove" @mouseleave="handleMouseLeave">
    <div class="logo" :class="{ 'mix-blend-lighten': showHalo, 'mix-blend-normal': !showHalo, 'opacity-[textOpacity]': true }" :style="{ maskImage: showHalo ? `radial-gradient(circle at ${haloLeft}px ${haloTop}px, black 75%, transparent 100%)` : 'none' }">
      中南研究院
    </div>
    <div v-if="showHalo" class="halo" :style="{ left: `${haloLeft}px`, top: `${haloTop}px` }"></div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const showHalo = ref(false);
const haloLeft = ref(0);
const haloTop = ref(0);
const textOpacity = ref(1);

const handleMouseMove = (event: MouseEvent) => {
  showHalo.value = true;
  haloLeft.value = event.clientX;
  haloTop.value = event.clientY;
  // 计算文字透明度，使文字在光标附近变亮
  const distance = Math.sqrt((event.clientX - window.innerWidth / 2) ** 2 + (event.clientY - window.innerHeight / 2) ** 2);
  textOpacity.value = Math.max(0, 1 - distance / 2000);
};

const handleMouseLeave = () => {
  showHalo.value = false;
  textOpacity.value = 1;
};
</script>

<style scoped>
.logo {
  @apply text-8xl font-bold text-center text-white select-none transition-all ease-linear duration-300;
}

.halo {
  @apply absolute blur-[160px] rounded-full opacity-50 -translate-x-2 -translate-y-2 pointer-events-none;
  background: repeating-linear-gradient(to right, #ff0c0c 0%, #e34c4c 50%, #d7a7a7 100%);
  height: 332px;
  width: 332px;
  transform: translate(-50%, -50%);
}
</style>
