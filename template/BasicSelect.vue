<script setup>
import { reactive, onMounted } from "vue";
const emits = defineEmits(["update:modelValue", "selected"]);

const props = defineProps({
  list: {
    type: Array,
    default: () => {
      return [];
    },
  },
  modelValue: {
    type: String,
    default: "",
  },
  roundedOption: {
    type: String,
    default: "left",
  },
});

const select = reactive({
  isSelectList: false,
  selectedSearchData: {},
  canSelectList: [],

  setIsSelectList: () => {
    select.isSelectList = !select.isSelectList;
  },
  setSelectedSearchData: async (value) => {
    emits("update:modelValue", value.value);
    emits("selected", value);
    select.selectedSearchData = value;
  },
});

onMounted(() => {
  select.canSelectList = props.list;
  select.selectedSearchData = props.list.find((item) => item.value === props.modelValue);
});
</script>

<template>
  <div
    :class="{
      'rounded-tl-md rounded-bl-md rounded-tr-md rounded-br-md': roundedOption === 'full',
      'rounded-tl-md rounded-bl-md': roundedOption === 'left',
      'rounded-tr-md rounded-br-md ': roundedOption === 'right',
    }"
    class="relative border border-solid border-[#D7DCE5]"
  >
    <button
      @focus="select.setIsSelectList"
      @focusout="select.setIsSelectList"
      class="flex items-center gap-2.5 p-3 cursor-pointer min-w-[110px] justify-between"
    >
      <p class="text-sm text-[#1C1E23]">{{ select.selectedSearchData.text }}</p>
      <img src="@/assets/img/select-arrow.png" alt="icon" class="w-2" />
    </button>

    <div v-if="select.isSelectList" class="absolute bg-white top-[52px] left-0 w-full z-[3]">
      <ul class="p-1 border border-solid border-[#D7DCE5] rounded shadow-[0_10px_20px_rgba(0,0,0,0.10)]">
        <li
          v-for="canSelect in select.canSelectList"
          :key="canSelect.value"
          @mousedown="select.setSelectedSearchData(canSelect)"
          class="text-sm text-[#1C1E23] px-2 py-2.5 hover:text-[#396CF1] hover:bg-[#EFF5FF] cursor-pointer"
        >
          {{ canSelect.text }}
        </li>
      </ul>
    </div>
  </div>
</template>
<style scoped lang="scss"></style>
