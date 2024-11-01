<template>
    <div class="mt-2 w-full space-y-2 ">
        <h1 class="text-[17px] text-[#181919] font-[600]">{{ label }}*</h1>
        <input :v-model={ItemModel} class="rounded-[15px] border border-black  outline-none h-[50px] w-full px-3" id="ItemId" :type="ItemType" />
    </div>
    <span id={ItemError} class="error">vvvhhv</span>
</template>

<script>
export default {
    name: "FormItem",
    props: {
        label: {
            type: String,
            required: true
        },
        ItemId: {
            type: String,
            required: true
        },
        ItemType: {
            type: String,
            default: "text"
        },
        ItemError: {
            type: String,
            required: true
        },
        ItemModel: {
            type: String,
            required: true
        }
    }
}
</script>

<style>
h1 {
    font-family: "Open Sans", sans-serif;
}
.error {
    color: red;
    font-size: 14px;
    margin-top: 2px;
}
</style>
