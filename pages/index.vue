<script setup lang="ts">
import LogoWithHalo from "~/pages/components/LogoWithHalo.vue";
import LogoWithHaloInTailwind from "~/pages/components/logoWithHaloInTailwind.vue";

const route = useRoute()
</script>

<template>
  <div class="main-container">
<!--    <LogoWithHalo/>-->
    <LogoWithHaloInTailwind/>
  </div>
</template>

<style scoped>
.main-container {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}
</style>
<style>
body {
  margin: 0;
}
</style>
