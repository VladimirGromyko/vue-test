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
    <h1>Страница с постами</h1>
    <div class="app__btns">
      <my-input
          v-model="searchQuery"
          placeholder="Поиск...."
      />
      <my-button @click="showDialog"
      >
        Создать пост
      </my-button>
      <my-select
          v-model="selectedSort"
          :options="sortOptions"
      />
    </div>
    <my-button @click="fetchPosts">Получить посты</my-button>
    <!--    <input type="text" v-model.trim="modificatorValue">-->

    <my-dialog v-model:show="dialogVisible">
      <PostForm
          @create="createPost"
          :filter="filter"
      />
    </my-dialog>

    <!--    Если сортируем с участием наблюдателя (свойство - watch)-->
    <!--    <PostList :posts="posts"-->
    <!--              @remove="removePost"-->
    <!--              v-if="!isPostsLoading"-->
    <!--    />-->

    <!--    Если сортируем с участием свойства - computed (сортируем до момента рендеринга)-->
    <PostList :posts="sortedAndSearchedPosts"
              @remove="removePost"
              v-if="!isPostsLoading"
    />
    <div v-else>Идет загрузка...</div>
    <div class="page__wrapper">
      <div v-for="pageNumber in totalPage"
           :key="pageNumber"
           class="page"
           :class="{
             'current-page': page===pageNumber
           }"
           @click="changePage(pageNumber)"
      >
        {{ pageNumber }}
      </div>
    </div>
    <GoodsList
        :product="product"
        :image="image"
        :link="link"
        :inventory="inventory"
        :onSale="onSale"
        :details="details"
        :cart="cart"
        :addToCart="addToCart"
        :variants="variants"
        :updateProduct="updateProduct"
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
import image1 from './assets/vmSocks-blue-onWhite.jpg'
import image2 from './assets/vmSocks-green-onWhite.jpg'
import MyDialog from "@/components/UI/MyDialog";
import axios from "axios";
import MySelect from "@/components/UI/MySelect";

export default {
  components: {
    MySelect,
    MyDialog,
    PostForm, PostList, GoodsList,
  },
  data() {
    return {
      // likes: 5,
      // dislikes: 1,
      posts: [
        // {id: 1, title: 'Javascript', body: 'Javascript универсальный язык программирования'},
        // {id: 2, title: 'Javascript', body: 'Описание поста 2'},
        // {id: 3, title: 'Typescript 3', body: 'Описание поста 3'},
        // {id: 4, title: 'Java 4', body: 'Описание поста 4'},
      ],
      dialogVisible: false,
      isPostsLoading: false,
      // modificatorValue: '',
      // title: '',
      // body: '',
      product: 'Socks',
      //

      image: image2, //'https://www.vuemastery.com/images/challenges/vmSocks-green-onWhite.jpg',
      link: 'https://www.amazon.com/s/ref=nb_sb_noss?url=search-alias%3Daps&field-keywords=socks',
      inventory: 12,
      onSale: true,
      details: ['80% cotton', '20% polyester', 'Gender-neutral'],
      variants: [
        {
          variantId: 2234,
          variantColor: "green",
          variantImage: image1,
        },
        {
          variantId: 2235,
          variantColor: "blue",
          variantImage: image2
        },

      ],
      cart: 0,
      selectedSort: '',
      searchQuery: '',
      page: 1,
      limit: 10,
      totalPage: 0,
      sortOptions: [
        {value: 'title', name: 'По названию'},
        {value: 'body', name: 'По содержимому'},
        {value: 'id', name: 'По идентификатору'},
      ],
    }
  },
  methods: {
    // addLike() {
    //   this.likes += 1
    // },
    // addDislike() {
    //   this.dislikes += 1
    // },
    filter(posts) {
      this.posts = this.posts.filter((el) => el.title === 'Javascript')
    },

    createPost(post) {
      this.posts.push(post)
      this.dialogVisible = false

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
    removePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id)
    },
    showDialog() {
      this.dialogVisible = true
    },
    changePage(pageNumber){
      this.page = pageNumber
    },
    async fetchPosts() {
      try {
        this.isPostsLoading = true
        // setTimeout(async () => {
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts',
            {
              params: {
                _page: this.page,
                _limit: this.limit
              }
            })
        debugger
        this.totalPage = Math.ceil(response.headers['x-total-count'] / this.limit)
        this.posts = response.data
        // this.isPostsLoading = false
        // }, 1000)
      } catch (e) {
        alert("Ошибка!")
      } finally {
        this.isPostsLoading = false
      }
    },


    updateProduct(variantImage) {
      this.image = variantImage
    },
    addToCart() {
      return this.cart += 1
    },
    // inputTitle(e){
    //   this.title=e.target.value
    //   // console.log(e)
    // }
  },
  mounted() {
    this.fetchPosts()
  },
  computed: {
    sortedPosts() {
      return [...this.posts].sort(
          (post1, post2) => String(post1[this.selectedSort])?.localeCompare(String(post2[this.selectedSort]))
      )
    },
    sortedAndSearchedPosts() {
      return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
    }
  },
  watch: {
    selectedSort(newValue) {
      // console.log(newValue)
      this.posts.sort((post1, post2) => {
        return String(post1[newValue])?.localeCompare(String(post2[newValue]))
      })
    },
    dialogVisible(newValue) {
      // console.log(newValue)
    },
    page(){
      this.fetchPosts()
    }
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

.app__btns {
  display: flex;
  justify-content: space-between;
  margin: 15px 0;
}

.page__wrapper {
  display: flex;
  margin-top: 15px;
}

.page {
  border: 1px solid black;
  padding: 10px;
  margin: 5px;
  border-radius: 15px;
}

.current-page {
  border: 2px solid teal;
}
</style>

<!--Video: https://www.youtube.com/watch?v=XzLuMtDelGk-->
<!--time:1:44:00-->
<!--Lessons:  https://habr.com/ru/company/ruvds/blog/509700/-->
