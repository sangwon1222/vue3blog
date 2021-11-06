<script setup lang="ts">
import { defineProps, ref, onMounted, onBeforeUpdate } from "vue";
const prop = defineProps<{
  login: string;
  login_guide: string;
  signup: string;
  signup_guide: string;
  loginmode: boolean;
}>();

let title = ref(null);
let buttonLabel = ref(null);
let buttonLink = ref(null);

onBeforeUpdate(() => {
  prop.loginmode ? signInMode() : signUpMode();
});
const signInMode = () => {
  title = prop.login_guide;
  buttonLabel = prop.login;
  buttonLink = "Login";
  console.log(buttonLink);
};
const signUpMode = () => {
  title = prop.signup_guide;
  buttonLabel = prop.signup;
  buttonLink = "SignUp";
  console.log(buttonLink);
};
</script>

<template>
  <div id="wrap">
    <h4>{{ title }}</h4>
    <router-link class="btn text bold" :to="{ name: buttonLink }">
      {{ buttonLabel }}
    </router-link>
  </div>
</template>

<style lang="scss" scoped>
.btn {
  position: relative;
  padding: 1rem;
  border-radius: 1rem;
  color: $sub_color;
  &:before {
    content: "";
    display: block;
    position: absolute;
    top: 50%;
    left: -0.1rem;
    width: 1rem;
    height: 2px;
    background: $sub_color;
    transform: translate(-50%, -50%);
  }
}
// pc
@media (min-width: 801px) {
}
// mobile
@media (max-width: 800px) {
}
</style>
