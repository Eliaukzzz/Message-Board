<template>
  <comments-app></comments-app>
</template>

<script lang="ts">
import { defineComponent } from "@vue/runtime-core";
import CommentsApp from "./CommentsApp.vue";
export default defineComponent({
  name: "App",
  components: { CommentsApp },
  setup() {
    return {};
  },
});
</script>

<style></style>
