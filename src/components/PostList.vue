<template>
  <div v-if="posts.length > 0">
<!--  <div v-show="posts.length > 0">-->
    <h3 style="margin-top: 15px">Список пользователей</h3>
    <PostItem
        v-for="post in posts"
        :key="post.id"
        :post="post"
        @remove="$emit('remove', post)"
    />
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

</style>