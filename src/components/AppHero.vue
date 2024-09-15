<template>
  <div class="hero">
    <!-- Tampilan dekstop -->
    <div class="d-none d-md-block">
      <div class="row mt-4">
        <div class="col-md-6">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h2>
                <strong>Delicous Food Menu,</strong> <br />
                Your Gadget
              </h2>
              <p>Ayo segera pesan dan nikmati makanan favorit anda!</p>
              <router-link to="/FoodsView" class="btn btn-lg btn-primary"><b-icon-arrow-right></b-icon-arrow-right> Pesan</router-link>
            </div>
          </div>
        </div>
        <div class="col">
          <img src="../assets/apphero.png" width="100%" />
        </div>
      </div>
    </div>

    <!-- tampilan mobile -->
    <div class="d-sm-block d-md-none">
      <div class="row mt-4">
        <div class="col">
          <img src="../assets/apphero.png" width="100%" />
        </div>
        <div class="col-md-6 mb-3">
          <div class="d-flex h-100">
            <div class="justify-content-center align-items-center">
              <h2>
                <strong>Delicous Food Menu,</strong> <br />
                Your Gadget
              </h2>
              <p>Ayo segera pesan dan nikmati makanan favorit anda!</p>
              <router-link to="/FoodsView" class="btn btn-lg btn-primary"><b-icon-arrow-right></b-icon-arrow-right> Pesan</router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AppHero",
};
</script>

<style></style>
