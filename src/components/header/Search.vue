<script setup lang="ts">
import { defineEmits } from "vue";
import GuideText from "@/types/GuideText";
import config from "@/utils";

const guide = config.guide_text[config.language];
const emit = defineEmits<{ (e: "close"): void }>();
const close = () => emit("close");

const clickSearch = () => {
  alert("검색기능 준비중입니다.");
};
</script>
<template>
  <div id="search-wrap">
    <button class="close" @click="close" />
    <input type="text" placeholder="검색어를 작성해주세요." maxlength="30" />
    <button class="search-btn color-btn" @click="clickSearch">
      {{ guide.search }}
    </button>
  </div>
</template>

<style lang="scss" scoped>
#search-wrap {
  position: fixed;
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
  justify-content: center;
  align-content: center;
  width: 100%;
  height: 0;
  background-color: rgba(0, 0, 0, 0.9);
  white-space: wrap;
  animation: slide-up-down 0.5s forwards;
  z-index: 10;
  .close {
    position: fixed;
    top: 1rem;
    right: 1rem;
    width: 4rem;
    height: 4rem;
    box-sizing: border-box;
    &:before,
    &:after {
      content: "";
      display: block;
      position: absolute;
      top: 50%;
      left: 50%;
      width: 0.5rem;
      height: 3rem;
      background-color: $green_color;
      transition: all 0.25s;
    }
    &:before {
      transform: translate(-50%, -50%) rotate(45deg);
    }
    &:after {
      transform: translate(-50%, -50%) rotate(-45deg);
    }
    &:hover:before {
      background-color: $main_color;
      transform: translate(-50%, -50%) rotate(-45deg);
    }
    &:hover:after {
      background-color: $main_color;
      transform: translate(-50%, -50%) rotate(45deg);
    }
  }
  > input {
    padding: 1rem;
    max-width: 600px;
    width: 80%;
    font-size: 1.2rem;
    letter-spacing: -0.2rem;
    font-weight: 800;
    box-sizing: border-box;
  }
  .search-btn {
    margin-top: 3rem;
    max-width: 600px;
    width: 80%;
  }
}

@keyframes slide-up-down {
  from {
    height: 0;
  }
  to {
    height: 100%;
  }
}
// pc
@media (min-width: 801px) {
}
// mobile
@media (max-width: 800px) {
}
</style>
