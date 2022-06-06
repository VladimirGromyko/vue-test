<template>
  <form @submit.prevent>
    <h4>Создание поста</h4>
    <!--        v-bind:value="post.title"-->
    <!--        @input="post.title=$event.target.value"-->
    <my-input
        v-model="post.title"
        type="text"
        placeholder="Название"
    />
    <!--    v-bind:value="post.body"-->
    <!--    @input="post.body=$event.target.value"    -->
    <my-input
        v-model="post.body"
        type="text"
        placeholder="Описание"
    />
    <div class="buttons">
      <my-button
          style="margin-top: 15px"
          @click="createPost"
      >Создать
      </my-button>
      <my-button
          style="margin-top: 15px"
          @click="filter"
      >Вывести только JS
      </my-button>
    </div>

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
  },
  watch: {
    // для примера - глубокое отслеживание
    post: {
      handler(newValue) {
        // console.log(newValue)
      },
      deep: true
    }
  }
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}


.buttons {
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
}

</style>