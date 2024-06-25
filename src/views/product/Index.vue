<template>
  <div>
    <div id="page-wrap">
      <div class="grid-wrap">
        <productItem v-for="product in products" :key="product.id" :product="product" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import ProductItem from "../../components/ProductItem";

export default {
  components: {
    ProductItem,
  },
  data() {
    return {
      products: [],
    };
  },
  async created() {
    const result = await axios.get("http://localhost:8000/api/products");
    this.products = result.data;
  },
};
</script>

<style scoped>
.grid-wrap {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  gap: 14px;
  margin-top: 16px;
}

/* Media query untuk desktop */
@media (min-width: 1024px) {
  .product-item {
    flex: 1 1 calc(33.333% - 16px); /* Tiga kolom dengan gap */
  }
}
</style>
