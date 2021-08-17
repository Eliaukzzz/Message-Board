<template>
  <main class="p-4 bg-gray-50 min-h-screen">
    <div class="max-w-screen-xl mx-auto bg-white p-8 rounded-lg shadow-2xl">
      <h2 class="text-3xl my-6">苍术的留言板</h2>
      <!-- 发布留言区 -->
      <comment-box
        @submit="addNewComment"
        :placeholder="`请留下你的足迹`"
      ></comment-box>
      <!-- 分割线 -->
      <divider-horizontal></divider-horizontal>
      <!-- 单个留言 -->
      <div v-for="comment in comments" :key="comment.id">
        <comment-item
          :user="comment.user"
          :avatar="comment.avatar"
          :time="comment.time"
          :content="comment.content"
        ></comment-item>
        <!-- 留言回复 -->
        <reply-container v-if="comment.replies">
          <comment-item
            v-for="reply in comment.replies"
            :key="reply.id"
            :user="reply.user"
            :avatar="reply.avatar"
            :time="reply.time"
            :content="reply.content"
          >
          </comment-item>
        </reply-container>
        <!-- 回复留言按钮 -->
        <comment-reply-box @submit="addReply($event, comment.id)" />
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent, ref } from "@vue/runtime-core";
import CommentBox from "./components/CommentBox.vue";
import DividerHorizontal from "./components/DividerHorizontal.vue";
import CommentItem from "./components/CommentItem.vue";
import CommentReplyBox from "./components/CommentReplyBox.vue";
import ReplyContainer from "./components/ReplyContainer.vue";

import face2 from "./assets/face2.jpg";

interface replyProp {
  id: number;
  user: string;
  avatar?: string;
  time: string;
  content: string;
}

interface commentProp {
  id: number;
  user: string;
  avatar: string;
  time: string;
  content: string;
  replies: replyProp[];
}
const comments = ref<commentProp[]>([
  {
    id: 1,
    user: "苍术",
    avatar: face2,
    time: "2小时以前",
    content: "啊我是猪",
    replies: [
      {
        id: 2,
        user: "苍术",
        avatar: face2,
        time: "2小时以前",
        content: "雀食",
      },
      {
        id: 3,
        user: "苍术",
        avatar: face2,
        time: "2小时以前",
        content: "你说的都对 你知道为什么吗",
      },
    ],
  },
  {
    id: 4,
    user: "苍术",
    avatar: face2,
    time: "2小时以前",
    content: "啊我是猪",
    replies: [
      {
        id: 5,
        user: "苍术",
        avatar: face2,
        time: "2小时以前",
        content: "雀食",
      },
    ],
  },
]);

export default defineComponent({
  components: {
    CommentBox,
    DividerHorizontal,
    CommentItem,
    CommentReplyBox,
    ReplyContainer,
  },
  setup() {
    let rid = ref(6);
    const constructNewComment = (content: string): commentProp => {
      return {
        id: rid.value++,
        user: "苍术",
        avatar: face2,
        content,
        time: "1秒前",
        replies: [],
      };
    };
    const constructNewReply = (content: string): replyProp => {
      return {
        id: rid.value++,
        user: "苍术",
        avatar: face2,
        content,
        time: "1秒前",
      };
    };
    const addNewComment = (content: string) => {
      const newComment = constructNewComment(content);
      comments.value.push(newComment);
    };
    const addReply = (content: string, id: number) => {
      const reply = constructNewReply(content);
      let comment = comments.value.find((comment) => comment.id === id);
      comment?.replies?.push(reply);
    };
    return {
      comments,
      constructNewComment,
      addNewComment,
      addReply,
    };
  },
});
</script>

<style></style>
