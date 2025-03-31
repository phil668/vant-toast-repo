<script setup lang="ts">
import { closeToast, showToast } from "vant";
import { ref } from "vue";

const isShowPopup = ref(false);

const onClickPopup = () => {
  console.log("click show popup");
  const toast = document.querySelector(".van-toast");
  if (toast) {
    console.log("toast display", getComputedStyle(toast).display);
  }
  isShowPopup.value = true;
};

const onClickToast = async () => {
  showToast({
    duration: 0,
    forbidClick: true,
    message: "Loading...",
    // 此处设置none的原因是不需要过渡效果，因此传none覆盖掉vant原有的默认过渡
    transition: "none",
  });

  await new Promise((resolve) => setTimeout(resolve, 3000));

  closeToast();
};
</script>

<template>
  <van-button @click="onClickToast">show toast</van-button>

  <van-button @touchstart="onClickPopup">show popup</van-button>

  <van-popup
    v-model:show="isShowPopup"
    title="Terms"
    position="bottom"
    round
    :close-on-click-overlay="false"
    transition=""
    closeable
    :style="{ height: '30%' }"
  >
  </van-popup>
</template>
