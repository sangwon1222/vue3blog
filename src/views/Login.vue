<script setup lang="ts">
import config from "@/utils";
import axios from "axios";
import { useRouter } from "vue-router";
import SocialLogin from "@/components/mypage/SocialLogin.vue";
import SignInOrUp from "../components/mypage/SignInOrUp.vue";

const guideText = config.guide_text[config.language];
const router = useRouter();

const getId = () => {
  const idInput = document.getElementById("idInput") as HTMLInputElement;
  if (idInput.value === "") {
    alert(`아이디를 작성해주세요.`);
    idInput.focus();
    return false;
  } else {
    return true;
  }
};

const getPassword = () => {
  const passwordInput = document.getElementById(
    "passwordInput"
  ) as HTMLInputElement;
  if (passwordInput.value === "") {
    alert(`비밀번호를 작성해주세요.`);
    passwordInput.focus();
    return false;
  } else {
    return true;
  }
};

const submitLogin = async () => {
  const id = (document.getElementById("idInput") as HTMLInputElement).value;
  const pw = (document.getElementById("passwordInput") as HTMLInputElement)
    .value;

  if (getId() === false) return;
  if (getPassword() === false) return;
  const userInfo = {
    username: id,
    password: pw,
  };

  try {
    const token = await axios({
      method: "post",
      url: "/api/auth/login",
      headers: { "Cache-Control": "no-cache" },
      data: userInfo,
    });
    console.log(token);
    localStorage.setItem("token", token.headers.authorization);
    localStorage.setItem("id", userInfo.username);
    router.push({ name: "MyPage" });
  } catch (error) {
    // console.groupCollapsed(`axios error`);
    // console.group(error);
    // console.groupEnd();

    alert("아직 회원이 아닙니다!");
    router.push({ name: "SignUp" });
  }
};
</script>

<template>
  <div id="login">
    <div class="sub-section">sub</div>
    <div class="main-section">
      <h2>{{ guideText.login }}</h2>

      <div class="input_wrap">
        <label class="text bold"> {{ guideText.id }} </label>
        <input id="idInput" class="input" type="text" />
      </div>
      <div class="input_wrap">
        <label class="text bold"> {{ guideText.password }} </label>
        <input id="passwordInput" class="input" type="password" />
      </div>

      <button
        class="login-btn color-btn text bold column-gap1"
        @click="submitLogin"
      >
        {{ guideText.login }}
      </button>

      <!-- 소셜로 로그인 -->
      <SocialLogin :socialText="guideText.socialText" />

      <!-- sign up -->
      <SignInOrUp
        :login="guideText.login"
        :login_guide="guideText.login_guide"
        :signup="guideText.signup"
        :signup_guide="guideText.signup_guide"
        :loginmode="false"
      />
    </div>
  </div>
</template>

<style lang="scss" scoped>
#login {
  overflow: hidden;
  position: relative;
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  .sub-section {
    border: 2px #000 solid;
    box-sizing: border-box;
  }
  .main-section {
    overflow: hidden;
    display: flex;
    flex-wrap: wrap;
    flex-direction: column;
    align-content: center;
    padding: 2rem 0 4rem;
    box-sizing: border-box;
  }
  .input_wrap {
    display: flex;
    flex-wrap: wrap;
    margin: 0 auto;
    width: 24rem;
    > label {
      display: flex;
      flex-wrap: wrap;
      justify-content: flex-start;
      align-items: center;
      flex: 0.3;
    }
    .input {
      flex: 1;
      padding: 0.5rem;
      border: 2px $sub-color solid;
      margin: 1rem;
    }
  }

  .login-btn {
    margin: 2rem auto;
    width: 8rem;
  }
}
// pc
@media (min-width: 801px) {
  #login {
    flex-direction: row;
    .sub-section {
      width: 50%;
      height: 100%;
    }
    .main-section {
      padding: 4rem 2rem;
      width: 50%;
      height: 100%;
    }
  }
}
// mobile
@media (max-width: 800px) {
  #login {
    align-items: center;
    .sub-section {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100vh;
      z-index: 0;
    }
    .main-section {
      width: 100%;
      height: 50%;
      background-color: #fff;
      z-index: 1;
    }
  }
}
</style>
