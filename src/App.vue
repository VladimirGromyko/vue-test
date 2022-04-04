<template>
  <div class="app">
    <!--    <div>-->
    <!--      <button @click="addLike">Like</button>-->
    <!--      <button @click="addDislike">Dislike</button>-->
    <!--    </div>-->
    <!--    <div>Количество лайков: <strong>{{likes}}</strong></div>-->
    <!--    <div>Количество лайков: <strong>{{dislikes}}</strong></div>-->

    <!--    <form @submit.prevent>-->
    <!--      <h4>Создание поста</h4>-->
    <!--      <input-->
    <!--          v-bind:value="title"-->
    <!--          @input="title=$event.target.value"-->
    <!--          class="input"-->
    <!--          type="text"-->
    <!--          placeholder="Название"-->
    <!--      >-->
    <!--      <input-->
    <!--          v-bind:value="body"-->
    <!--          @input="body=$event.target.value"-->
    <!--          class="input"-->
    <!--          type="text"-->
    <!--          placeholder="Описание"-->
    <!--      >-->
    <!--      <button-->
    <!--          class="btn"-->
    <!--          @click="createPost"-->
    <!--      >Создать-->
    <!--      </button>-->
    <!--    </form>-->
    <!--    <div class="post" v-for="post in posts">-->
    <!--      <div><strong>Название:</strong> {{ post.title }}</div>-->
    <!--      <div><strong>Описание:</strong> {{ post.body }}</div>-->
    <!--    </div>-->
    <PostForm @create="createPost"/>
    <PostList :posts="posts"/>
    <GoodsList
        :product="product"
        :image="image"
        :link="link"
        :inventory="inventory"
        :onSale="onSale"
        :details="details"
    />
    <!--    <GoodsList-->
    <!--        :product="product"-->
    <!--        :image="image"-->
    <!--        :link="link"-->
    <!--        :inventory="inventory"-->
    <!--        :onSale="onSale"-->
    <!--        :details="details"-->
    <!--        :variants="variants"-->
    <!--        @filter="filter"-->
    <!--    />-->

  </div>
</template>

<script>

import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import GoodsList from "@/components/GoodsList";

export default {
  components: {
    PostForm, PostList, GoodsList,
  },
  data() {
    return {
      // likes: 5,
      // dislikes: 1,
      posts: [
        {id: 1, title: 'Javascript', body: 'Javascript универсальный язык программирования'},
        {id: 2, title: 'Javascript', body: 'Описание поста 2'},
        {id: 3, title: 'Typescript 3', body: 'Описание поста 3'},
        {id: 4, title: 'Java 4', body: 'Описание поста 4'},
      ],
      // title: '',
      // body: '',
      product: 'Socks',
      //

      image: 'https://www.vuemastery.com/images/challenges/vmSocks-green-onWhite.jpg',
      link: 'https://www.amazon.com/s/ref=nb_sb_noss?url=search-alias%3Daps&field-keywords=socks',
      inventory: 12,
      onSale: true,
      details: ['80% cotton', '20% polyester', 'Gender-neutral'],
      // variants: [
      //   {
      //     variantId: 2234,
      //     variantColor: "green"
      //   },
      //   {
      //     variantId: 2235,
      //     variantColor: "blue"
      //   },

    }
  },
  methods: {
    // addLike() {
    //   this.likes += 1
    // },
    // addDislike() {
    //   this.dislikes += 1
    // },
    filter() {
      this.posts = this.posts.filter((el) => el.title === 'Javascript')
    },

    createPost(post) {
      this.posts.push(post)

      // e.stopPropagation()
      // e.preventDefault()
      // const newPost = {
      //   id: Date.now(),
      //   title: this.title,
      //   body: this.body,
      // }
      // this.posts.push(newPost)
      // this.title = ''
      // this.body = ''
      // this.posts = [...this.posts, newPost]
    },
    // inputTitle(e){
    //   this.title=e.target.value
    //   // console.log(e)
    // }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  padding: 20px;
}

/*.post {*/
/*  padding: 15px;*/
/*  border: 2px solid teal;*/
/*  margin-top: 15px;*/
/*}*/


/*form {*/
/*  display: flex;*/
/*  flex-direction: column;*/
/*}*/

/*.input {*/
/*  width: 100%;*/
/*  border: 1px solid teal;*/
/*  padding: 10px 15px;*/
/*  margin-top: 15px;*/
/*}*/

/*.btn {*/
/*  margin-top: 15px;*/
/*  align-self: flex-end;*/
/*  padding: 10px 15px;*/
/*  background: none;*/
/*  color: teal;*/
/*  border: 1px solid teal;*/
/*  border-radius: 10px;*/
/*}*/
.product {
  display: flex;
}

img {
  border: 1px solid #d8d8d8;
  width: 70%;
  margin: 40px;
  box-shadow: 0px .5px 1px #d8d8d8;
}

.product-image {
  flex-basis: 700px;
}

.product-info {
  margin-top: 10px;
  flex-basis: 500px;
}


</style>

<!--Video: https://www.youtube.com/watch?v=XzLuMtDelGk-->
<!--time: 46.47-->
<!--Lessons:  https://habr.com/ru/company/ruvds/blog/509700/-->