<template>
<div>
  <nav class="navbar navbar-expand-lg">
  <div class="container-fluid">
    <a class="navbar-brand" href="#"><img src="~assets/img/logo.png" style="width:100px;"></a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav me-auto mb-2 mb-lg-0">
        <li class="nav-item mx-3">
          <nuxt-link to="../"><h5 style="color:black;">MENU</h5></nuxt-link>
        </li>
        <li class="nav-item">
        <nuxt-link to="/statistik/"><h5 style="color:black;">STATISTIK</h5></nuxt-link>
        </li>
      </ul>
    </div>
  </div>
</nav>
</div>
</template>
<style scoped>
.navbar{
  font-family: inter;
  background-color: #c78800;
}
</style>


