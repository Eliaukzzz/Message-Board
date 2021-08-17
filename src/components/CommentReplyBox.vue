<template>
  <button
    class="pt-4 text-blue-600"
    :class="[showCommentbox ? 'pb-2' : 'pb-10']"
    @click.prevent="showCommentbox = !showCommentbox"
  >
    回复
  </button>
  <comment-box
    v-if="showCommentbox"
    :placeholder="`评论些什么吧`"
    class="mb-4"
    @submit="handleSubmit"
  />
</template>

<script lang="ts">
import { defineComponent, ref } from "@vue/runtime-core";
import CommentBox from "./CommentBox.vue";

export default defineComponent({
  emits: ["submit"],
  components: {
    CommentBox,
  },
  setup(_props, context) {
    const showCommentbox = ref(false);
    const handleSubmit = (e: string) => {
      context.emit("submit", e);
      showCommentbox.value = false;
    };
    return {
      showCommentbox,
      handleSubmit,
    };
  },
});
</script>

<style></style>
