<template>
  <div>
    <h3>Список пользователей</h3>
    <PostItem
        v-for="post in posts"
        :key="post.id"
        :post="post"
    />
  </div>
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