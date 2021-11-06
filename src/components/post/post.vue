<script setup lang="ts">
import PostList from "@/types/PostList";
import { defineProps } from "vue";

const prop = defineProps<{
  img: string;
  title: string;
  writer: string;
  writeDate: string;
  likeCnt: number;
}>();
</script>
<template>
  <div id="post">
    <div class="img-stage">
      <img :src="prop.img" alt="포스트 이미지" />
    </div>

    <div class="title-stage">
      {{ prop.title }}
    </div>

    <div class="writer-stage">
      <div class="writer">by. {{ prop.writer }}</div>
      <div class="date">{{ prop.writeDate }}</div>
    </div>

    <div class="like-stage">
      <div class="emoji">👍</div>
      <div class="like-cnt">{{ prop.likeCnt }}</div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
#post {
  overflow: hidden;
  position: relative;
  box-sizing: border-box;

  .img-stage {
    overflow: hidden;
    position: relative;
    width: 100%;
    > img {
      position: absolute;
      transform: translate(-50%, -50%);
      top: 50%;
      left: 50%;
      width: 100%;
    }
  }
}

// pc
@media (min-width: 901px) {
  #post {
    .img-stage {
      height: 20rem;
    }
  }
}
// tablet
@media (max-width: 900px) and (min-width: 701px) {
  #post {
    .img-stage {
      height: 20rem;
    }
  }
}

// mobile
@media (max-width: 700px) {
  #post {
    .img-stage {
      height: 20rem;
    }
  }
}
</style>
