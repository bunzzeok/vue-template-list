<template>
  <Transition name="fade">
    <div
      v-if="isShow"
      class="w-full h-full fixed top-0 left-0 bg-opacity-30 bg-black flex items-center justify-center z-[9999]"
      @click="closeConfirm(false)"
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
        <div>확인</div>
      </div>
      <div class="h-[80%] pt-1 break-words">
        {{ message }}
      </div>
      <div class="h-[10%] pt-2 flex items-center justify-end gap-3">
        <button
          @click="closeConfirm(true)"
          class="px-3 py-1.5 text-white bg-blue-500 rounded-xl cursor-pointer"
        >
          확인
        </button>
        <button
          @click="closeConfirm(false)"
          class="px-3 py-1.5 text-white bg-red-500 rounded-xl cursor-pointer"
        >
          취소
        </button>
      </div>
    </div>
  </Transition>
</template>
<script setup>
import { inject } from "vue";

// inject 로 제공하는것을 가져오기
const { isShow, message, closeConfirm } = inject("basicConfirm");
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
