<template>
  <div v-if="posts.length > 0">
<!--  <div v-show="posts.length > 0">-->
    <h3 style="margin-top: 15px">Список пользователей</h3>
    <transition-group name="post-list">
      <PostItem
          v-for="post in posts"
          :key="post.id"
          :post="post"
          @remove="$emit('remove', post)"
      />
    </transition-group>

  </div>
  <h3 v-else style="color: red">
<!--  <h2 v-show="posts.length === 0" style="color: red">-->
    Список пользователей пуст
  </h3>
</template>

<script>
import PostItem from "@/components/PostItem";

export default {
  name: "PostList",
  components: {PostItem},
  props: {
    posts: {
      type: [],
      required: true
    }
  }
}
</script>

<style scoped>
.post-list-item {
  display: inline-block;
  margin-right: 10px;
}
.post-list-enter-active,
.post-list-leave-active {
  transition: all 0.4s ease;
}
.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateX(130px);
}
.post-list-move {
  transition: transform 0.4s ease;
}
</style>