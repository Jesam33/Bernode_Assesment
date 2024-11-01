<template>
  <div>
    <h1 
      class="text-[17px] font-[600]" 
      :class="{'text-red-500': hasError}"
    >
      {{ label }}*
    </h1>
    <input
      :type="ItemType || 'text'"
      v-model="localValue"
      :class="[
        'rounded-[15px] border border-black outline-none h-[50px] w-full px-3', 
        {'border-red-500': hasError}
      ]"
      :id="ItemId"
    />
    <p class="error" v-if="ItemError">{{ ItemError }}</p>
  </div>
</template>

<script>
export default {
  name: "FormItem",
  props: {
    label: String,
    ItemId: String,
    ItemType: String,
    ItemError: String,
    modelValue: String,
  },
  data() {
    return {
      localValue: this.modelValue, // Initialize with the prop value
    };
  },
  computed: {
    hasError() {
      return !!this.ItemError; // Returns true if there's an error
    }
  },
  watch: {
    // Watch the prop for changes and update localValue accordingly
    modelValue(newValue) {
      this.localValue = newValue;
    },
    // Watch localValue and emit the change to the parent
    localValue(newValue) {
      this.$emit("update:modelValue", newValue);
    },
  },
};
</script>

<style>
.error {
  color: red;
  font-size: 14px;
  font-weight: 600;
  margin-top: 10px;
}
</style>
