<script setup lang="ts">
import { onMounted, ref } from "vue";
import config from "@/utils";
import GuideText from "@/types/GuideText";
import Search from "@/components/header/Search.vue";
import gsap from "gsap";

let pcflag = false;
const mobileflag = ref(false);

let guide: GuideText = config.guide_text[config.language];
onMounted(() => {
  guide = config.guide_text[config.language];
  window.addEventListener("resize", () => {
    innerWidth > 800 ? resetMobileList() : resetPcList();
  });
});

const clickList = () => {
  const mobilebtn = document.getElementById("checkbox") as HTMLInputElement;
  mobilebtn.checked ? showMobileList() : hideMobileList();
};
// 돋보기 클릭.
const clickSearch = () => {
  resetMobileList();
  innerWidth > 800 ? pcSearch() : mobileSearch();
};

const resetList = () => {
  resetMobileList();
  resetPcList();
};

// pc
const resetPcList = () => {
  pcflag = false;
  hidePcSearch();
};
const pcSearch = () => {
  pcflag = !pcflag;
  pcflag ? showPcSearch() : hidePcSearch();
};
const showPcSearch = () => {
  const pcSearchScreen = document.getElementsByClassName("pc-search")[0];
  pcSearchScreen && gsap.to(pcSearchScreen, { height: "auto", duration: 0.25 });
};
const hidePcSearch = () => {
  const pcSearchScreen = document.getElementsByClassName("pc-search")[0];
  pcSearchScreen && gsap.to(pcSearchScreen, { height: "0", duration: 0.25 });
};

const resetMobileList = () => {
  const mobilebtn = document.getElementById("checkbox");
  mobilebtn ? ((mobilebtn as HTMLInputElement).checked = false) : null;
  hideMobileList();
  mobileflag.value = false;
};

const showMobileList = () => {
  const mobileList = document.getElementsByClassName("btn-wrap")[0];
  gsap.to(mobileList, { height: "auto", duration: 0.25 });
};

const hideMobileList = () => {
  const mobileList = document.getElementsByClassName("btn-wrap")[0];
  mobileList && gsap.to(mobileList, { height: "3rem", duration: 0.25 });
};
const closeSearch = () => {
  mobileflag.value = false;
};
const mobileSearch = () => {
  mobileflag.value = !mobileflag.value;
};
</script>

<template>
  <div id="header">
    <Search v-if="mobileflag" @close="closeSearch" />

    <div class="header-wrap wrap">
      <!-- 로고 -->
      <div @click="resetList">
        <router-link class="logo-wrap" :to="{ name: 'Home' }">
          <img src="@/assets/logo.png" class="logo" alt="logo" />
        </router-link>
      </div>

      <div class="btn-wrap">
        <!-- 모바일일때 헤더의 버튼 리스트 -->
        <input type="checkbox" id="checkbox" class="list" @click="clickList" />

        <!-- 검색버튼 -->
        <div class="search icon" @click="clickSearch" />

        <!-- 나의페이지버튼 -->
        <div @click="resetList">
          <router-link class="mypage icon" :to="{ name: 'MyPage' }" />
        </div>
      </div>
    </div>

    <div class="pc-search wrap">
      <input type="text" placeholder="검색어를 작성해주세요." />
      <button class="search" @click="resetPcList">
        {{ guide?.search }}
      </button>
    </div>
  </div>
</template>

<style lang="scss" scoped>
#header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 9;
  background-color: $main_color;
  .header-wrap {
    position: relative;
    display: flex;
    flex-wrap: wrap;
    align-content: center;
    .logo-wrap {
      overflow: hidden;
      display: flex;
      flex-wrap: wrap;
      align-content: center;
      .logo {
        width: 100%;
      }
    }

    .btn-wrap {
      box-sizing: border-box;
      background-color: $main_color;
      z-index: 2;

      .icon {
        overflow: hidden;
        display: block;
        position: relative;
        width: 3rem;
        height: 3rem;
        cursor: pointer;
      }
      .search {
        &:before,
        &:after {
          content: "";
          display: block;
          position: absolute;
          top: 50%;
          left: 50%;
          box-sizing: border-box;
        }
        &:before {
          margin: 0.7rem 0 0 0.7em;
          width: 0.2rem;
          height: 0.5rem;
          transform: translate(-50%, -50%) rotate(-45deg);
          background-color: $sub_color;
        }
        &:after {
          width: 1.4rem;
          height: 1.4rem;
          transform: translate(-50%, -50%);
          background-color: $main_color;
          border: 0.2rem $sub_color solid;
          border-radius: 2rem;
        }
        &:hover:before {
          animation: moveCenter 0.25s 0.1s forwards;
        }
        &:hover:after {
          animation: moveCenter 0.25s forwards;
        }
      }
      .mypage {
        &:before,
        &:after {
          content: "";
          display: block;
          position: absolute;
          top: 50%;
          left: 50%;
          box-sizing: border-box;
          border-radius: 100%;
          transform: translate(-50%, -50%);
        }
        &:before {
          margin-top: 0.5rem;
          width: 2rem;
          height: 1rem;
          border: 0.2rem $sub_color solid;
          border-bottom: none;
        }
        &:after {
          margin-top: -0.2rem;
          width: 1rem;
          height: 1rem;
          border: 0.2rem $sub_color solid;
          background-color: $main_color;
        }
        &:hover:before {
          animation: moveCenter 0.25s forwards;
        }
        &:hover:after {
          animation: moveCenter 0.25s 0.1s forwards;
        }
      }
    }
  }
}

//pc
@media (min-width: 801px) {
  #header {
    .header-wrap {
      justify-content: space-between;
      height: 100px;
      .logo-wrap {
        width: 12rem;
      }
      .btn-wrap {
        display: flex;
        flex-wrap: wrap;
        align-items: center;
        justify-content: space-between;
        .icon {
          margin: 0 0.4rem;
        }
        .list {
          display: none;
        }
      }
    }
    .pc-search {
      overflow: hidden;
      display: block;
      margin: 0 auto;
      height: 0;
      white-space: wrap;
      > input {
        padding: 1rem;
        margin: 1rem;
        max-width: 1000px;
        width: 70%;
      }
      .search {
        float: right;
        margin: 1rem;
        padding: 1rem 2rem;
        background: $sub_color;
        color: $green_color;
        border-radius: 0.5rem;
      }
    }
  }
}

// mobile
@media (max-width: 800px) {
  #header {
    .header-wrap {
      justify-content: center;
      height: 80px;
      .logo-wrap {
        width: 8rem;
        animation: moveCenter 0.25s forwards;
      }
      .btn-wrap {
        overflow: hidden;
        position: absolute;
        top: 1rem;
        right: 0;
        height: 3rem;
        .icon {
          margin: 0.8rem auto;
        }
        .list {
          position: relative;
          display: block;
          margin: 0 auto;
          width: 3rem;
          height: 3rem;
          cursor: pointer;
          box-sizing: border-box;
          background-color: none;
          appearance: none;
          padding: 0;
          border: none;
          &:checked:before {
            position: absolute;
            top: 50%;
            left: 50%;
            margin: 0;
            width: 2rem;
            height: 0rem;
            border: none;
            border-top: 0.2rem $green_color solid;
            border-bottom: 0.2rem $green_color solid;
            transform: translate(-50%, -50%) rotate(45deg);
          }
          &:checked:after {
            position: absolute;
            top: 50%;
            left: 50%;
            margin-top: 0;
            width: 2rem;
            height: 0.35rem;
            background-color: $green_color;
            transform: translate(-50%, -50%) rotate(-45deg);
          }
          &:before,
          &:after {
            content: "";
            display: block;
            margin: 0 auto;
          }
          &:before {
            margin-top: 0.5rem;
            width: 2rem;
            height: 0.2rem;
            border-top: 0.4rem $sub_color solid;
            border-bottom: 0.4rem $sub_color solid;
            transition: all 0.25s, border-color 0.25s 0.5s;
          }
          &:after {
            margin-top: 0.25rem;
            width: 2rem;
            height: 0.35rem;
            background-color: $sub_color;
            transition: all 0.5s, background-color 0.25s 0.5s;
          }
        }
      }
    }
    .pc-search {
      display: none;
    }
  }
}
</style>
