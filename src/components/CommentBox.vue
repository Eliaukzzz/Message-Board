<template>
  <form action="" class="grid" @submit.prevent="handleSubmit">
    <textarea
      v-model="content"
      name="comment"
      id=""
      :placeholder="placeholder"
      class="bg-gray-50 p-2 rounded"
    ></textarea>
    <fieldset class="py-4">
      <input
        type="submit"
        value="评论"
        class="px-4 py-1 bg-blue-500 rounded text-white"
      />
      <input
        type="submit"
        value="取消"
        class="px-4 py-1 bg-white rounded border ml-3"
      />
    </fieldset>
  </form>
</template>

<script lang="ts">
import { defineComponent, ref } from "@vue/runtime-core";

export default defineComponent({
  props: {
    placeholder: {
      type: String,
    },
  },
  emits: ["submit"],
  setup(_props, context) {
    const content = ref("");
    const handleSubmit = () => {
      context.emit("submit", content.value);
      content.value = "";
    };
    return {
      content,
      handleSubmit,
    };
  },
});
</script>

<style></style>
