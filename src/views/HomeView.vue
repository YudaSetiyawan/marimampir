<template>
  <div class="home">
    <AppNavbar />,
    <div class="container">
      <AppHero />
      <div class="row mt-4">
        <div class="col">
          <h3>Best <strong>Foods</strong></h3>
        </div>
        <div class="col">
          <router-link to="/FoodsView" class="btn btn-primary float-right"><b-icon-eye></b-icon-eye> Lihat Semua</router-link>
        </div>
      </div>
      <div class="row mb-4">
        <div class="col-md-4 mt-4" v-for="product in products" :key="product.id">
          <CardProduct :product="product" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import AppNavbar from "@/components/AppNavbar.vue";
import AppHero from "@/components/AppHero.vue";
import CardProduct from "@/components/CardProduct.vue";
import axios from "axios";

export default {
  name: "HomeView",
  components: {
    AppNavbar,
    AppHero,
    CardProduct,
  },
  data() {
    return {
      products: [],
    };
  },
  methods: {
    setProduct(data) {
      this.products = data; // Mengubah data products
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/best-products")
      .then((response) => this.setProduct(response.data)) // Menggunakan setProduct
      .catch((error) => console.log(error));
  },
};
</script>
