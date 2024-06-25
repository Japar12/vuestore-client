<template>
  <div class="product-item">
    <img :src="`http://localhost:8000${product.imageUrl}`" alt="" />
    <h3 class="product-name">{{ product.name }}</h3>
    <p class="product-price">Rp{{ product.price }}</p>
    <router-link :to="{ name: 'product-detail', params: { id: product.code } }">
      <button>Details</button>
    </router-link>
  </div>
</template>

<script>
export default {
  props: ["product"],
};
</script>

<style scoped>
.product-item {
  align-items: center;
  border-radius: 8px;
  box-shadow: 0px 2px 5px #888;
  display: flex;
  flex-direction: column;
  margin-bottom: 2%;
  padding: 20px;
  position: relative;
  width: 32%;
  box-sizing: border-box; /* Pastikan padding tidak mempengaruhi lebar elemen */
}

.product-name {
  margin-bottom: 0;
  text-align: center;
  
}

img {
  max-width: 100%; /* Gambar mengikuti lebar parent */
  height: auto; /* Mengatur tinggi secara otomatis sesuai aspek gambar */
  border-radius: 5%;
}

a {
  width: 100%;
}

button {
  width: 100%;
  padding: 10px;
  font-size: 16px;
} 
/* Media query untuk tablet */
@media (max-width: 768px) {
  .product-item {
    width: 48%; /* Dua kolom dengan gap */
  }

  img {
    height: 150px;
  }
}

/* Media query untuk ponsel */
@media (max-width: 480px) {
  .product-item {
    width: 100%; /* Satu kolom penuh */
  }

  img {
    height: 120px;
  }
}

/* Media query untuk desktop */
@media (min-width: 1024px) {
  .product-item {
    flex: 1 1 calc(33.333% - 16px); /* Tiga kolom dengan gap */
  }
}
</style>
