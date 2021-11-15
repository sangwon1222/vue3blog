<script setup lang="ts">
import config from "@/utils";
import { onMounted } from "@vue/runtime-core";
import Post from "./post.vue";

const data = config.testDummy;
onMounted(() => {
  //   console.log(data);
});
</script>
<template>
  <div id="post-group">
    <div class="post-wrap wrap">
      <div v-for="(v, i) in data" :key="i" class="post">
        <Post
          :img="v.img"
          :title="v.title"
          :writer="v.writer"
          :writeDate="v.writeDate"
          :likeCnt="v.likeCnt"
        />
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
#post-group {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-content: center;
  .post-wrap {
    overflow: hidden;
    display: flex;
    flex-wrap: wrap;
    width: 100%;
    box-sizing: border-box;
    .post {
      overflow: hidden;
      padding: 1rem;
      box-sizing: border-box;
      transition: flex-basis 0.5s;
    }
  }
}

// pc
@media (min-width: 1001px) {
  #post-group {
    .post-wrap {
      .post {
        flex-basis: 33.33%;
      }
    }
  }
}
// tablet
@media (max-width: 1000px) and (min-width: 701px) {
  #post-group {
    .post-wrap {
      .post {
        flex-basis: 50%;
      }
    }
  }
}

// mobile
@media (max-width: 700px) {
  #post-group {
    .post-wrap {
      .post {
        flex-basis: 100%;
      }
    }
  }
}
</style>
