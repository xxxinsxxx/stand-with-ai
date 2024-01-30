<template>
  <!-- 页面结构 -->
  <div class="relative w-full h-screen flex justify-center items-center bg-black overflow-hidden" @mousemove="handleMouseMove" @mouseleave="handleMouseLeave">
    <!-- Logo 文字区域 -->
    <div class="logo" :class="{ 'mix-blend-lighten': showHalo, 'mix-blend-normal': !showHalo, 'opacity-[textOpacity]': true }" :style="{ maskImage: showHalo ? `radial-gradient(circle at ${haloLeft}px ${haloTop}px, black 75%, transparent 100%)` : 'none' }">
      中南研究院
    </div>
    <!-- 光圈效果区域 -->
    <div v-if="showHalo" class="halo" :style="{ left: `${haloLeft}px`, top: `${haloTop}px` }"></div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

// 响应式数据
const showHalo = ref(false); //是否应显示光标周围的光晕效果
const haloLeft = ref(0); //光晕效果的水平位置
const haloTop = ref(0); //光晕效果的垂直位置
const textOpacity = ref(1); //徽标内文本的不透明度

// 处理鼠标移动事件
const handleMouseMove = (event: MouseEvent) => {
  showHalo.value = true;
  haloLeft.value = event.clientX;
  haloTop.value = event.clientY;
  // 计算文字透明度，使文字在光标附近变亮
  const distance = Math.sqrt((event.clientX - window.innerWidth / 2) ** 2 + (event.clientY - window.innerHeight / 2) ** 2);
  textOpacity.value = Math.max(0, 1 - distance / 2000);
};

// 处理鼠标离开事件
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
