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
<!--        <div>-->
          <div v-for="variant in variants"
               :key="variant.variantId">
<!--            <p @mouseover="updateProduct(variant.variantImage)">-->
              {{ variant.variantColor }}
<!--            </p>-->
          </div>
<!--        </div>-->
        <div class="basket">
          <!--              v-on:click="cart += 1"-->
          <MyButton
              class="btn"
              @click="addToCart"
          >Add to cart
          </MyButton>
          <div class="basket__cart">
            <p>Cart({{ cart }})</p>
          </div>
        </div>

      </div>
    </div>

  </div>
</template>

<script>
import MyButton from "@/components/UI/MyButton";

export default {
  name: "GoodsList",
  components: {MyButton},
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
    variants: {
      type: [
        // {
        //   variantId: {type:Number, required:true},
        //   variantColor: {type:String, required:true},
        //   variantImage: {type:String, required:true},
        // }
      ],
      required: true,
    },
    cart: {
      type: Number,
      required: true
    },
    addToCart: {
      type: Function,
      required: true
    },
    updateProduct: {
      type: Function,
      required: true
    }
  },

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

.basket {
  display: flex;

  flex-direction: row;
  justify-content: space-between;
}

.basket__cart {
  border: 1px solid #d8d8d8;
  margin-top: 15px;
  padding: 10px 15px;
}
</style>