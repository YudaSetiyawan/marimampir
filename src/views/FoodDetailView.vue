<template>
  <div class="Foods-Detail">
    <AppNavbar />
    <div class="container">
      <!-- breadcrumb -->
      <div class="row mt-3">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link to="/" class="text-dark">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link to="/FoodsView" class="text-dark">Foods</router-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">Foods Order</li>
            </ol>
          </nav>
        </div>
      </div>

      <!-- food detail -->
      <div class="row mt-3">
        <div class="col-md-6">
          <img :src="'../assets/images/' + product.gambar" class="img-fluid shadow" alt="" />
        </div>
        <div class="col-md-6 py-0">
          <h2>
            <strong>{{ product.nama }}</strong>
          </h2>
          <h5>
            Harga <strong>Rp. {{ product.harga }}</strong>
          </h5>
          <form class="border-top py-3" v-on:submit.prevent>
            <div class="form-group">
              <label for="jumlah_pemesanan">Jumlah Pemesanan</label>
              <input type="number" class="form-control" v-model="pesan.jumlah_pemesanan" />
            </div>
            <div class="form-group">
              <label for="keterangan">Catatan Khusus</label>
              <textarea v-model="pesan.keterangan" type="text" placeholder="Masukan catatan khusus: Pedes, Nasi setengah, dll" class="form-control font-italic"></textarea>
            </div>
            <div class="form-group">
              <label for="nomor_meja">Nama/Nomor Meja</label>
              <input type="text" class="form-control" v-model="pesan.nomor_meja" />
            </div>
          </form>
          <button @click="pemesanan" type="submit" class="btn btn-primary float-right"><b-icon-cart></b-icon-cart> Pesan</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import AppNavbar from "@/components/AppNavbar.vue";
import axios from "axios";

export default {
  name: "FoodsDetailView",
  components: {
    AppNavbar,
  },
  data() {
    return {
      product: {},
      pesan: {},
    };
  },
  methods: {
    setProduct(data) {
      this.product = data; // Mengubah data products
    },
    pemesanan() {
      if (this.pesan.jumlah_pemesanan) {
        this.pesan.products = this.product;
        axios
          .post("http://localhost:3000/keranjangs", this.pesan)
          .then(() => {
            this.$router.push({ path: "/KeranjangView" });
            this.$toasted.show("Pesanan Sukses", {
              duration: 3000,
            });
          })
          .catch((err) => console.log(err));
      } else {
        this.pesan.products = this.product;
        axios
          .post("http://localhost:3000/keranjangs", this.pesan)
          .then(() => {
            this.$toasted.show("Pesanan Tidak Sesuai", {
              duration: 3000,
            });
          })
          .catch((err) => console.log(err));
      }
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/products/" + this.$route.params.id)
      .then((response) => this.setProduct(response.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style></style>
