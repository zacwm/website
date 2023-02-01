<script setup>
import MainBox from './components/MainBox.vue'
</script>

<template>
  <div class="parentbox">
    <MainBox />
  </div>
</template>

<style scoped>
  .parentbox {
    display: block;
    height: 100vh;
    width: 100vw;
    padding: 60px;
  }
</style>