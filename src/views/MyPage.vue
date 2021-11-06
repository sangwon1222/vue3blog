<script setup lang="ts">
import { onBeforeMount } from "@vue/runtime-core";
import { useRouter } from "vue-router";

onBeforeMount(() => {
  const tocken = localStorage.getItem("token");
  const router = useRouter();
  !tocken && router.push({ name: "Login" });
});
</script>
<template>
  <div id="mypage">mypage</div>
</template>

<style lang="scss" scoped></style>
