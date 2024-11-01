<template>
  <div class="mt-2 w-full space-y-2 ">
    <h1 class="text-[17px] text-[#181919] font-[600]">{{ label }}*</h1>
    <select :id="ItemId" :type="ItemType"  class=" border border-black rounded-[15px] rounded-[15px] h-[50px] w-full px-3">
      <option
      class="border border-black"
        v-for="(option, index) in options"
        :key="index"
        :value="option.value"
      >
        {{ option.label }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: "SelectFormItem",
  props: {
    options: {
      type: Array,
      required: true,
    },
    label: {
      type: String,
      required: true,
    },
    ItemId: {
      type: String,
      required: true,
    },
    ItemType: {
      type: String,
      default: "text",
    },
  },
};
</script>

<style>
h1 {
  font-family: "Open Sans", sans-serif;
}
</style>