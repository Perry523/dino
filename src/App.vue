<template>
  <RouterView style="display: none" />
</template>

<script setup>
import { RouterView } from 'vue-router'
</script>
<style>
#app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
body {
  background-color: #f7f7f7;
}
</style>
