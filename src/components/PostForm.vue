<template>
  <form @submit.prevent>
    <h4>Создание поста</h4>
    <!--        v-bind:value="post.title"-->
    <!--        @input="post.title=$event.target.value"-->
    <input
        v-model="post.title"
        class="input"
        type="text"
        placeholder="Название"
    >
    <!--    v-bind:value="post.body"-->
    <!--    @input="post.body=$event.target.value"    -->
    <input
        v-model="post.body"
        class="input"
        type="text"
        placeholder="Описание"
    >
    <button
        class="btn"
        @click="createPost"
    >Создать
    </button>
  </form>
</template>

<script>
export default {
  name: "PostForm",
  data() {
    return {
      post: {
        title: '',
        body: '',
      }
    }
  },
  methods: {
    createPost() {
      // const newPost = {
      //   id: Date.now(),
      //   title: this.title,
      //   body: this.body,
      // }
      this.post.id = Date.now()
      this.$emit('create', this.post)
      this.post = {
        title: '',
        body: '',
      }
      // this.posts.push(newPost)
      // this.title = ''
      // this.body = ''
    }
  }
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}

.input {
  width: 100%;
  border: 1px solid teal;
  padding: 10px 15px;
  margin-top: 15px;
}

.btn {
  margin-top: 15px;
  align-self: flex-end;
  padding: 10px 15px;
  background: none;
  color: teal;
  border: 1px solid teal;
  border-radius: 10px;
}
</style>