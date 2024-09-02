<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-12 col-lg-8 col-md-8 col-sm-12 my-4">
        <form @submit.prevent="getMenu" class="d-flex mx-5 mb-4 px-5">
          <input v-model="keyword" class="form-control rounded-pill" type="search"
            placeholder="Mau Beli Apaa ...........?" aria-label="Search">
        </form>
        <div class="row">
          <div class="col-12 col-lg-4 col-md-6 col-sm-12 mb-4">
            <div class="card shadow rounded-4">
              <div class="img p-2">
                <img src="~assets/img/baso.jpg" class="card-img-top rounded-3" alt="cover"
                  style="height: 150px; object-fit: cover;">
              </div>
              <div class="card-body">
                <div class="d-flex justify-content-between mb-2">
                  <div class="font-weight-bold"><b>baso</b></div>
                  <div>4000</div>
                </div>
                <button class="btn rounded-4" style="background-color: #c78800; width: 95%;">
                  <i class="bi bi-cart mx-4"></i>
                </button>
              </div>
            </div>
          </div>
          <div class="col-12 col-lg-4 col-md-6 col-sm-12 mb-4">
            <div class="card shadow rounded-4">
              <div class="img p-2">
                <img src="~assets/img/baso.jpg" class="card-img-top rounded-3" alt="cover"
                  style="height: 150px; object-fit: cover;">
              </div>
              <div class="card-body">
                <div class="d-flex justify-content-between mb-2">
                  <div class="font-weight-bold"><b>baso</b></div>
                  <div>4000</div>
                </div>
                <button class="btn rounded-4" style="background-color: #c78800; width: 95%;">
                  <i class="bi bi-cart mx-4"></i>
                </button>
              </div>
            </div>
          </div>
          <div class="col-12 col-lg-4 col-md-6 col-sm-12 mb-4">
            <div class="card shadow rounded-4">
              <div class="img p-2">
                <img src="~assets/img/baso.jpg" class="card-img-top rounded-3" alt="cover"
                  style="height: 150px; object-fit: cover;">
              </div>
              <div class="card-body">
                <div class="d-flex justify-content-between mb-2">
                  <div class="font-weight-bold"><b>baso</b></div>
                  <div>4000</div>
                </div>
                <button class="btn rounded-4" style="background-color: #c78800; width: 95%;">
                  <i class="bi bi-cart mx-4"></i>
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="col-12 col-lg-4 d-flex justify-content-center align-items-start my-4 shadow">
        <div class="order-summary mt-4" style="width: 90%;">
          <div class="card rounded-5 shadow mb-2">
            <div class="card-body" style="font-size: 120%;">
              <b>
                <div class="container">
                  <div class="row item-row align-items-center">
                    <div class="col-md-6">BASO</div>
                    <div class="col-md-4 text-right">2</div>
                    <div class="col-md-2 text-center">
                      <button class="btn btn-trash" aria-label="Delete item">
                        <i class="bi bi-trash-fill"></i>
                      </button>
                    </div>
                  </div>
                </div>
              </b>
            </div>
          </div>
          <div class="card-body text-center">
            <hr>
            <h5 class="card-title">TOTAL PRICE <span>8000</span></h5>
            <button class="btn chekout py-3 mt-3 rounded-5" style="width: 100%; background-color: #c78800;">
              <h4><b>ORDER</b></h4>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
definePageMeta({
  middleware: 'auth'
})
let user = useSupabaseUser()
console.log(user)
</script>