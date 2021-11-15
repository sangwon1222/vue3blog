<script setup lang="ts">
import UserInfo from "@/types/UserInfo";
import { onBeforeMount, ref } from "vue";
import axios from "axios";
import { useRouter } from "vue-router";
import myInfo from "@/components/mypage/myIntro.vue";
import myPost from "@/components/mypage/myPost.vue";

const userInfo = ref(null);
const currentList = ref(0);
const list = [
  {
    id: 0,
    text: "글",
  },
  {
    id: 1,
    text: "소개",
  },
];
const clickList = (info) => {
  console.log(info);
  currentList.value = info.id;
};
const router = useRouter();

onBeforeMount(async () => {
  // const id = localStorage?.getItem("id");
  // if (!id) {
  //   router.push({ name: "Login" });
  //   return;
  // }
  // await axios({
  //   method: "get",
  //   url: `api/user/${id}`,
  // })
  //   .then((response) => {
  //     console.log(response);
  //     userInfo.value = response.data;
  //     if (response.data.lastName === null) userInfo.value.lastName = "name";
  //   })
  //   .catch((error) => {
  //     console.log(error);
  //   });
});
</script>
<template>
  <div id="mypage">
    <div class="profile">
      <div class="img">사진</div>
      <ul class="name row">
        <li>이름</li>
        <li class="left1">{{ userInfo?.lastName }}</li>
      </ul>
      <ul class="follow row">
        <li>팔로워 수</li>
        <li class="left1">0</li>
      </ul>
    </div>

    <div class="nav wrap">
      <div
        v-for="(v, i) in list"
        :key="i"
        class="list bold"
        @click="clickList(v)"
      >
        {{ v.text }}
      </div>
    </div>

    <myPost v-show="currentList == 0" />
    <myInfo v-show="currentList == 1" />
  </div>
</template>

<style lang="scss" scoped>
#mypage {
  .profile {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    margin: 10px auto;
    width: 800px;
    .img {
      overflow: hidden;
      width: 100px;
      height: 100px;
      border: 2px rgba(0, 0, 0, 0.2) solid;
    }
  }
  .nav {
    display: flex;
    .list {
      padding: 1rem 0;
      font-size: 1.1rem;
      background-color: $sub_color;
      color: $main_color;
      box-sizing: border-box;
      cursor: pointer;
      &:hover {
        background-color: $main_color;
        color: $sub_color;
      }
    }
  }
}
// pc
@media (min-width: 801px) {
  .nav {
    flex-direction: row;
    justify-content: space-evenly;
    .list {
      width: 50%;
    }
  }
}
// mobile
@media (max-width: 800px) {
  .nav {
    flex-direction: column;
    justify-content: space-evenly;
    .list {
      width: 100%;
    }
  }
}
</style>
