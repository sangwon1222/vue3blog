<script setup lang="ts">
import config from "@/utils";
import { ref } from "vue";

const registIntroFlag = ref(false);
const infoBtnText = ref(config.guide_text[config.language].writeGreeting);

const openRegist = () => {
  registIntroFlag.value = true;
  infoBtnText.value = config.guide_text[config.language].editGreeting;
  console.log(`openRegist`);
};
const editRegist = () => {
  registIntroFlag.value = false;
  infoBtnText.value = config.guide_text[config.language].writeGreeting;
  console.log(`editRegist`);
};

const clickRegistBtn = () => {
  registIntroFlag.value ? editRegist() : openRegist();
};
</script>
<template>
  <div id="myIntro">
    <h3>{{ config.guide_text[config.language].noGreeting }}</h3>
    <button class="basic-btn bold btn" @click="clickRegistBtn">
      {{ infoBtnText }}
    </button>
  </div>
</template>

<style lang="scss" scoped>
// pc
@media (min-width: 801px) {
}
// mobile
@media (max-width: 800px) {
}
</style>
