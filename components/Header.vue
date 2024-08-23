<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-light">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">
          <img src="~assets/img/logo.png" alt="Logo" style="width:100px;">
        </a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item mx-3">
              <nuxt-link to="../" class="nav-link">
                <h5 class="mb-0">MENU</h5>
              </nuxt-link>
            </li>
            <li class="nav-item">
              <nuxt-link to="/statistik" class="nav-link">
                <h5 class="mb-0">STATISTIK</h5>
              </nuxt-link>
            </li>
          </ul>
          <form class="d-flex ms-auto">
            <input class="form-control rounded-pill" type="search" placeholder="Mau Beli Apaa ...........?" aria-label="Search">
          </form>
        </div>
      </div>
    </nav>
  </div>
</template>

<style scoped>
.navbar {
  font-family: 'Inter', sans-serif;
  background-color: #c78800;
}

.nav-link {
  color: black;
}

.nav-link:hover {
  color: #fff; /* Ganti warna saat hover */
}

.form-control {
  width: 500px; 
}
</style>
