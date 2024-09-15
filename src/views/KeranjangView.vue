<template>
  <div class="keranjangview">
    <AppNavbar :updateKeranjang="keranjangs" />
    <div class="container">
      <div class="row mt-4">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link to="/" class="text-dark">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link to="/FoodsView" class="text-dark">Foods</router-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">Keranjang</li>
            </ol>
          </nav>
        </div>
      </div>

      <div class="row">
        <div class="col">
          <h2>Keranjang <strong>Pesanan</strong></h2>
          <table class="responsive mt-3">
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">#</th>
                  <th scope="col">Foto</th>
                  <th scope="col">Makanan</th>
                  <th scope="col">Jumlah Pemesanan</th>
                  <th scope="col">Catatan Khusus</th>
                  <th scope="col">Nama/Meja</th>
                  <th scope="col">Harga</th>
                  <th scope="col">Total Harga</th>
                  <th scope="col">Hapus</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(keranjang, index) in keranjangs" :key="keranjang.id">
                  <th>{{ index + 1 }}</th>
                  <td><img :src="'../assets/images/' + keranjang.products.gambar" class="img-fluid shadows" width="150" /></td>
                  <td>
                    <strong>{{ keranjang.products.nama }}</strong>
                  </td>
                  <td>{{ keranjang.jumlah_pemesanan }}</td>
                  <td>{{ keranjang.keterangan ? keranjang.keterangan : "-" }}</td>
                  <td>{{ keranjang.nomor_meja }}</td>
                  <td align="right">Rp. {{ keranjang.products.harga }}</td>
                  <td align="right">
                    <strong>Rp. {{ keranjang.products.harga * keranjang.jumlah_pemesanan }}</strong>
                  </td>
                  <td align="center" class="text-danger">
                    <b-icon-trash @click="hapusKeranjang(keranjang.id)"></b-icon-trash>
                  </td>
                </tr>
                <br />
                <tr>
                  <td colspan="7" align="right">
                    <strong>Total Harga:</strong>
                  </td>
                  <td align="right">
                    <strong>Rp. {{ totalHarga }}</strong>
                  </td>
                </tr>
              </tbody>
              <tr>
                <td colspan="8">
                  <div class="d-flex justify-content-end">
                    <button @click="checkout" type="submit" class="btn btn-success">Checkout</button>
                  </div>
                </td>
              </tr>
            </table>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import AppNavbar from "@/components/AppNavbar.vue";
import axios from "axios";

export default {
  components: { AppNavbar },
  name: "KeranjangView",

  data() {
    return {
      keranjangs: [],
      pesan: [],
      pesanans: {},
    };
  },
  methods: {
    setKeranjangs(data) {
      this.keranjangs = data;
    },
    hapusKeranjang(id) {
      axios
        .delete("http://localhost:3000/keranjangs/" + id)
        .then(() => {
          // Hapus item dari daftar keranjangs setelah berhasil dihapus
          this.keranjangs = this.keranjangs.filter((item) => item.id !== id);
        })
        .catch((error) => {
          // Error handling (jika diperlukan)
          console.error("Error deleting item:", error);
        });
    },
    checkout() {
      // Membuat objek pesanans yang berisi keranjangs dan totalHarga
      const pesanans = {
        pesanans: this.keranjangs, // Data keranjangs yang akan dikirim
        totalHarga: this.totalHarga, // Menambahkan total harga jika diperlukan
      };

      // Mengirim data pesanans ke server
      axios
        .post("http://localhost:3000/pesanans/", pesanans) // Mengirim payload pesanan
        .then(() => {
          this.keranjangs.map(function (item) {
            return axios.delete("http://localhost:3000/keranjangs/" + item.id).catch((error) => console.log(error));
          });
          // Redirect ke halaman PesananSuksesView setelah sukses checkout
          this.$router.push({ path: "/PesananSuksesView" });
          this.$toasted.show("Sukses", { duration: 3000 }); // Notifikasi sukses
        })
        .catch((err) => console.log(err)); // Error handling
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/keranjangs")
      .then((response) => this.setKeranjangs(response.data))
      .catch((error) => console.log(error));
  },
  computed: {
    totalHarga() {
      return this.keranjangs.reduce((items, data) => {
        return items + data.products.harga * data.jumlah_pemesanan;
      }, 0);
    },
  },
};
</script>

<style></style>
