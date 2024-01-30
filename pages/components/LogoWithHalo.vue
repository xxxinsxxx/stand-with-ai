<template>
  <!-- 页面结构 -->
  <div class="logo-container" @mousemove="handleMouseMove" @mouseleave="handleMouseLeave">
    <!-- Logo 文字区域 -->
    <div class="logo" :style="{ maskImage: showHalo ? `radial-gradient(circle at ${haloLeft}px ${haloTop}px, black 75%, transparent 100%)` : 'none', mixBlendMode: showHalo ? 'lighten' : 'normal', opacity: textOpacity }">
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
/* 样式定义 */
.logo-container {
  position: relative;
  width: 100%;
  height: 100vh;
  overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #000;
}

.logo {
  font-size: 100px; /* 调整字体大小 */
  font-weight: bold;
  text-align: center;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5); /* 添加文字阴影效果 */
  transition: mix-blend-mode 0.3s ease, opacity 0.3s ease, mask-image 0.3s ease; /* 添加过渡效果 */
  user-select: none;
  color: #fff;
}

.halo {
  position: absolute;
  height: 332px;
  width: 332px;
  filter: blur(160px);
  border-radius: 50%;
  background: repeating-linear-gradient(to right, #ff0c0c 0%, #e34c4c 50%, #d7a7a7 100%);
  opacity: 0.5;
  transform: translate(-50%, -50%);
  pointer-events: none;
}
</style>
