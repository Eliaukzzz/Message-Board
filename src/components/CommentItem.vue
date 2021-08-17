<template>
  <div class="flex">
    <!-- /绝对路径代表public  -->
    <img :src="avatar" alt="" class="w-12 h-12 mr-4 rounded-full" />
    <div>
      <p>{{ user }}</p>
      <p class="text-gray-600 text-sm">{{ time }}</p>
    </div>

    <!-- 三点下拉菜单右对齐 -->
    <span class="ml-auto">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-5 w-5 text-gray-500"
        viewBox="0 0 20 20"
        fill="currentColor"
      >
        <path
          d="M10 6a2 2 0 110-4 2 2 0 010 4zM10 12a2 2 0 110-4 2 2 0 010 4zM10 18a2 2 0 110-4 2 2 0 010 4z"
        />
      </svg>
    </span>
  </div>
  <p class="text-gray-600 py-4">{{ content }}</p>
</template>

<script lang="ts">
import { defineComponent } from "@vue/runtime-core";

export default defineComponent({
  props: {
    user: {
      type: String,
      default: "苍术",
    },
    avatar: {
      type: String,
      default: "/images/1.jpg",
    },
    time: {
      type: String,
      default: "2小时以前",
    },
    content: {
      type: String,
    },
  },
  setup() {
    return {};
  },
});
</script>

<style></style>
