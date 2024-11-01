<template>
  <div>
    <label :for="ItemId" class="text-[17px] text-[#181919] font-[600] block mb-2">{{ label }}</label>
    <select :id="ItemId" v-model="selectedValue" class="rounded-[15px] border border-black outline-none h-[50px] w-full px-3" @change="updateValue">
      <option v-for="option in options" :key="option.value" :value="option.value">
        {{ option.label }}
      </option>
    </select>
    <span v-if="SelectItemError" class="text-red-500">{{ SelectItemError }}</span>
  </div>
</template>

<script>
export default {
  props: {
    label: String,
    ItemId: String,
    value: String,
    options: Array,
    SelectItemError: String,
  },
  computed: {
    selectedValue: {
      get() {
        return this.value; // Bind the select value to v-model
      },
      set(value) {
        this.$emit('input', value); // Emit the value back to the parent
      },
    },
  },
  methods: {
    updateValue(event) {
      this.selectedValue = event.target.value;
    },
  },
};
</script>

<style scoped>
/* Add any styles specific to your SelectFormItem here */
</style>
