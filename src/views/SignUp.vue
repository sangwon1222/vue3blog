<script setup lang="ts">
import axios from "axios";
import config from "@/utils";
import { onMounted } from "vue";
import { useRouter } from "vue-router";
import SocialLogin from "@/components/mypage/SocialLogin.vue";
import SignInOrUp from "../components/mypage/SignInOrUp.vue";

const guideText = config.guide_text[config.language];
const router = useRouter();

onMounted(() => {
  const telInput = document.getElementById("telInput") as HTMLInputElement;
  document.addEventListener("keydown", (e) => keyDownEnter(e), false);
  telInput.addEventListener("keyup", () => {
    let inputValue = telInput.value;
    telInput.value = inputValue.replace(/[^0-9]/gi, "");
  });
});

const keyDownEnter = (e) => {
  console.log(e.key);
  e.key === "Enter" && submitSignUp(), false;
};

const duplicateCheck = (obj: HTMLInputElement, kindOf: string) => {
  if (obj.value === "") {
    alert(`${kindOf} 작성하세요.`);
    obj.focus();
    return false;
  } else {
    return true;
  }
};

const submitSignUp = async () => {
  const id = document.getElementById("idInput") as HTMLInputElement;
  const pw = document.getElementById("passwordInput") as HTMLInputElement;
  const email = document.getElementById("emailInput") as HTMLInputElement;
  const tel = document.getElementById("telInput") as HTMLInputElement;
  if (duplicateCheck(id, guideText.id) === false) return;
  if (duplicateCheck(pw, guideText.password) === false) return;
  if (duplicateCheck(email, guideText.email) === false) return;
  if (duplicateCheck(tel, guideText.tel) === false) return;
  const userInfo = {
    username: id,
    password: pw,
    email: email,
    telNo: tel,
  };

  try {
    await axios({
      method: "post",
      url: "api/user",
      data: userInfo,
    });
    router.push({ name: "Login" });
  } catch (error) {
    console.groupCollapsed("axios error");
    console.group(error);
    console.groupEnd();

    router.push({ name: "Home" });
  }
};
</script>

<template>
  <div id="sign-up">
    <h2>
      {{ guideText.signup }}
    </h2>

    <div class="input_wrap">
      <label class="text bold"> {{ guideText.id }} </label>
      <input id="idInput" class="input" type="text" />
    </div>
    <div class="input_wrap">
      <label class="text bold"> {{ guideText.email }} </label>
      <input id="emailInput" class="input" type="text" />
    </div>
    <div class="input_wrap">
      <label class="text bold"> {{ guideText.password }} </label>
      <input id="passwordInput" class="input" type="password" />
    </div>
    <div class="input_wrap">
      <label class="text bold"> {{ guideText.tel }} </label>
      <input
        id="telInput"
        type="text"
        class="input"
        placeholder="- 없이 입력해주세요"
        maxlength="11"
      />
    </div>

    <button class="color-btn text bold column-gap1" @click="submitSignUp">
      {{ guideText.signup }}
    </button>

    <SocialLogin :socialText="guideText.socialText" />
    <SignInOrUp
      :login="guideText.login"
      :login_guide="guideText.login_guide"
      :signup="guideText.signup"
      :signup_guide="guideText.signup_guide"
      :loginmode="true"
    />
  </div>
</template>

<style lang="scss" scoped>
#sign-up {
  padding: 2rem 0;
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
}
// pc
@media (min-width: 801px) {
}
// mobile
@media (max-width: 800px) {
}
</style>
