<script setup lang="ts">
import Header from "@/components/header/Header.vue";
</script>
<template>
  <div id="app">
    <Header />
    <router-view />
  </div>
</template>

<style lang="scss" scoped>
#app {
  padding-top: 100px;
  text-align: center;
}
</style>
