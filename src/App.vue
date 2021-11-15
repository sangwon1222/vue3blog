<script setup lang="ts">
import Header from "@/components/header/Header.vue";
</script>
<template>
  <div id="app">
    <Header />
    <router-view />
    <!-- <a id="git" href="https://github.com/sangwon1222/vue3blog"
      >https://github.com/sangwon1222/vue3blog</a
    > -->
  </div>
</template>

<style lang="scss" scoped>
#app {
  padding-top: 100px;
  text-align: center;
}
#git {
  position: fixed;
  left: 0;
  bottom: 0;
  background-color: #fff;
  color: #000;
}
</style>
