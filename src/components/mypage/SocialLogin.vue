<script setup lang="ts">
import { defineProps } from "vue";

const prop = defineProps<{ socialText: string }>();
</script>

<template>
  <div id="social-login">
    <h4>{{ prop.socialText }}</h4>
    <ul class="social row">
      <li>git</li>
      <li>gmail</li>
      <li>kakao</li>
    </ul>
    <hr />
  </div>
</template>

<style lang="scss" scoped>
#social-login {
  width: 100%;
  justify-content: center;
  box-sizing: border-box;
  > h4 {
    padding: 1rem 0;
  }
  .social {
    width: 100%;
    justify-content: center;
    box-sizing: border-box;
    padding: 1rem 0 2rem;
    > li {
      overflow: hidden;
      display: flex;
      justify-content: center;
      align-items: center;
      margin: 0 1rem;
      width: 4rem;
      height: 4rem;
      border-radius: 100%;
      background: #fff;
      border: 2px $green_color solid;
    }
  }
}
// pc
@media (min-width: 801px) {
}
// mobile
@media (max-width: 800px) {
}
</style>
