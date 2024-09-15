<template>
  <div class="PesananSuksesView">
    <AppNavbar />
    <div class="container">
      <div class="row justify-content-center mt-5">
        <div class="col text-center">
          <img src="../assets/menunggu.png" width="150" />
          <h2><strong> Pesanan Sukses </strong></h2>
          <h3>Silahkan ditunggu, terima kasih.</h3>
          <router-link to="/" class="btn btn-primary mt-3">Selesai</router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import AppNavbar from "@/components/AppNavbar.vue";

export default {
  name: "PesananSuksesView",
  components: {
    AppNavbar,
  },
};
</script>

<style></style>
