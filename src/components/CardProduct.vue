<template>
  <div class="card text-center shadow card-product">
    <img :src="'assets/images/' + product.gambar" class="card-img-top" alt="..." />
    <div class="card-body">
      <h5 class="card-title">{{ product.nama }}</h5>
      <p class="card-text">{{ product.harga }}</p>
      <router-link class="btn btn-primary" :to="'/FoodsView/' + product.id"><b-icon-cart></b-icon-cart> Pesan</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardProduct",
  props: ["product"],
};
</script>

<style></style>
