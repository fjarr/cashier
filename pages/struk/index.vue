<template>
  <div class="judul d-flex justify-content-center mt-5">
    <h2>ANGKRINGAN BREE</h2>
  </div>
  <p class="d-flex justify-content-center">Jl. Lkr. Utara,Purbaratu kota.Tasikmalaya, Jawa Barat</p>
  <div class="container-fluid d-flex justify-content-center" id="i">
        <table class="table table-bordered" style="width: 85%">
          <thead>
            <tr class="fw-bold">
              <td>NAMA BARANG</td>
              <td style="width: 6%">JUMLAH</td>
              <td>HARGA BARANG</td>
              <td>TOTAL HARGA</td>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(item, i) in orderItems" :key="i">
              <td>{{ item.produk }}</td>
              <td>{{ item.quantity }}</td>
              <td>{{ item.harga.toLocaleString() }}</td>
              <td>{{ (item.harga * item.quantity).toLocaleString() }}</td>
            </tr>
          </tbody>
        </table>
      </div>
      <div class="total d-flex justify-content-center my-5">
        <table class="text-center" style="width: 85%; align-items: center">
          <tr class="fw-bold mb-5">
            <td>TOTAL ALL</td>
            <td>INPUT UANG</td>
            <td>TOTAL KEMBALIAN</td>
          </tr>
          <tr>
            <td>{{ totalbelanja.toLocaleString() }}</td>
            <td style="width: 20%; align-items: center">
              <input type="number" id="amountReceived" v-model.number="jumlahuang" class="form-control" placeholder="Berapa uang mu?" />
            </td>
            <td>{{ kembalian.toLocaleString() }}</td>
          </tr>
        </table>
      </div>
      <div class="print d-flex justify-content-end me-5">
        <button onclick="window.print()" class="btn btn-dark me-5">PRINT</button>
      </div>
</template>
<script setup>
useHead({ title: 'STRUK' });
definePageMeta({
  middleware: 'auth',
});
const orderItems = ref([]);
const totalbelanja = ref(0);
const jumlahuang = ref(0);
const kembalian = computed(() => {
  const total = totalbelanja.value;
  const uang = jumlahuang.value;
  return Math.max(uang - total, 0);
});
onMounted(() => {
  orderItems.value = JSON.parse(localStorage.getItem('orderItems'));
  totalbelanja.value = parseFloat(localStorage.getItem('totalbelanja'));
});
</script>
<style setup>
#i {
  margin-top: 2%;
}
@media (max-width: 820px) {
  #i {
    margin-top: 10%;
  }
}
</style>
