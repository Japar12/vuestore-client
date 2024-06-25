<template>
  <div>
    <div id="page-wrap">
      <h1>Shopping Cart</h1>
      <ItemCart v-for="item in cartItems" :key="item.id" :item="item" v-on:remove-item="removeFromCart($event)" />
      <h3 id="total-price">Total: Rp{{ totalPrice }}</h3>
      <button id="checkout-button">Checkout</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import ItemCart from "../../components/ItemCart.vue";

export default {
  components: {
    ItemCart,
  },
  data() {
    return {
      cartItems: [],
    };
  },
  methods: {
    async removeFromCart(product) {
      await axios.delete(`http://localhost:8000/api/orders/delete/user/1/product/${product}`);
      let cart = this.cartItems
        .map(function (item) {
          return item.code;
        })
        .indexOf(product);
      this.cartItems.splice(cart, 1);
      console.log(cart);
    },
  },
  computed: {
    totalPrice() {
      return this.cartItems.reduce((sum, item) => sum + Number(item.price), 0);
    },
  },
  async created() {
    const result = await axios.get(`http://localhost:8000/api/orders/user/1`);
    let data = Object.assign(
      {},
      ...result.data.map((result) => ({
        cart_items: result.products,
      }))
    );
    this.cartItems = data.cart_items;
  },
};
</script>

<style scoped>
h1 {
  border-bottom: 1px solid #41b883;
  margin: 0;
  margin-top: 16px;
  padding: 16px;
}
#page-wrap {
  margin: 0 auto;
  max-width: 1100px;
  padding: 16px;
  width: 100%;
}
#total-price {
  padding: 16px;
  text-align: right;
  font-size: 1.5rem;
}
#checkout-button {
  width: 100%;
  padding: 16px;
  font-size: 1rem;
}
@media (max-width: 768px) {
  h1 {
    font-size: 1.5rem;
  }

  #total-price {
    font-size: 1.2rem;
  }

  #checkout-button {
    font-size: 0.9rem;
    padding: 12px;
  }
}

@media (max-width: 480px) {
  h1 {
    font-size: 1.2rem;
    padding: 12px;
  }

  #total-price {
    font-size: 1rem;
    padding: 12px;
  }

  #checkout-button {
    font-size: 0.8rem;
    padding: 10px;
  }
}
</style>
