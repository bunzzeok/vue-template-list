<template>
  <Transition name="fade">
    <div
      v-if="isShow"
      class="w-full h-full fixed top-0 left-0 bg-opacity-30 bg-black flex items-center justify-center z-[9999]"
      @click="closeAlert()"
    ></div>
  </Transition>
  <Transition name="fade">
    <div
      v-if="isShow"
      class="top-1/2 left-1/2 -translate-y-2/4 -translate-x-2/4 fixed w-[400px] drop-shadow-2xl rounded-xl z-[10000] bg-white p-4"
    >
      <div
        class="h-[10%] font-semibold text-2xl flex items-center justify-between"
      >
        <div>알림</div>
        <img
          @click="closeAlert()"
          src="@/assets/img/close.png"
          alt=""
          class="w-4 h-4 cursor-pointer"
        />
      </div>
      <div class="h-[90%] pt-1 break-words">
        {{ message }}
      </div>
    </div>
  </Transition>
</template>
<script setup>
import { inject } from "vue";

// inject 로 제공하는것을 가져오기
const { isShow, message, closeAlert } = inject("basicAlert");
</script>
<style lang="scss">
.fade-enter-active,
.fade-leave-active {
  transition: all 0.1s ease-in-out;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0.1;
}
</style>
