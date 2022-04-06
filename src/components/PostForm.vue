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

    <!--    v-model="post.body"-->
    <input

        v-bind:value="post.body"
        @input="post.body=$event.target.value"
        class="input"
        type="text"
        placeholder="Описание"
    >
    <div class="buttons">
      <MyButton
          class="btn"
          @click="createPost"
      >Создать
      </MyButton>
      <MyButton
          class="btn"
          @click="filter"
      >Вывести только JS
      </MyButton>
    </div>

  </form>
</template>

<script>
import MyButton from "@/components/UI/MyButton";

export default {
  name: "PostForm",
  components: {MyButton},
  data() {
    return {
      post: {
        title: '',
        body: '',
      }
    }
  },
  props: ["filter"],

  // () {
  // this.posts = this.posts.filter((el) => el.title === 'Javascript')
  // },
  // },
  methods: {
    // filter() {
    //   this.posts = this.posts.filter((el) => el.title === 'Javascript')
    // },


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

.buttons {
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
}

</style>