<template>

  <div>
    <div class="product">
      <div class="product-image">
        <img :src="image"/>
        <a :href="link">More products like this</a>
      </div>
      <div class="product-info">
        <h1>{{ product }}</h1>
        <p v-if="inventory > 10">In stock</p>
        <p v-else-if="inventory <= 10 && inventory > 0">Almost sold out!</p>
        <p v-else>Out of stock</p>
        <span v-show="onSale">On sale!</span>
        <ul>
          <li v-for="detail in details">{{ detail }}</li>
        </ul>
      </div>
    </div>
<!--    <button-->
<!--        class="btn"-->
<!--        @click="filter"-->
<!--    >Вывести только JS-->
<!--    </button>-->
  </div>
</template>

<script>
export default {
  name: "GoodsList",
  props: {
    product: {
      type: String,
      required: true
    },
    image: {
      type: String,
      required: true
    },
    link: {
      type: String,
      required: true
    },
    inventory: {
      type: Number,
      required: true
    },
    onSale: {
      type: Boolean,
      required: true
    },
    details: {
      type: Array,
      required: true
    },
    // variants: {
    //   type: [
    //     {
    //       variantId: number,
    //       variantColor: string,
    //     }
    //   ],
    //   required: true,
    // },
  }
}
</script>

<style scoped>
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