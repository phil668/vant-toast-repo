<script setup lang="ts">
import { closeToast, showToast } from "vant";
import { ref } from "vue";

const showPopup = ref(false);

const popup = () => {
  console.log("click show popup");
  showPopup.value = true;
};

const toast = async () => {
  showToast({
    duration: 0,
    forbidClick: true,
    message: "Loading...",
    transition: "none",
  });

  await new Promise((resolve) => setTimeout(resolve, 3000));

  closeToast();
};
</script>

<template>
  <van-button @click="toast">show toast</van-button>

  <van-button @touchstart="popup">show popup</van-button>

  <van-popup
    v-model:show="showPopup"
    title="Terms"
    position="bottom"
    round
    :close-on-click-overlay="false"
    transition="none"
    closeable
    :style="{ height: '30%' }"
  >
  </van-popup>
</template>
