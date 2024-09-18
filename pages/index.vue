<template>
  <div class="container-fluid">
    <div class="row mt-1">
      <div class="col-12 col-lg-8 col-md-8 col-sm-12 my-4">
        <form @submit.prevent="getMenu" class="d-flex mx-5 mb-4 px-4" id="ic">
          <input v-model="keyword" class="form-control rounded-pill" type="search" placeholder="Mau Beli Apaa ...........?" aria-label="Search" />
          <i class="bi bi-cart-check ms-2" id="c" style="font-size: 30px"></i>
        </form>
        <div class="row">
          <div class="col-12 col-lg-4 col-md-6 col-sm-12 mb-4" v-for="(menu, i) in Menu" :key="i">
            <div class="card shadow rounded-4">
              <div class="img p-2">
                <img :src="menu.cover" class="card-img-top rounded-3" alt="cover" style="height: 150px; object-fit: cover" />
              </div>
              <div class="card-body">
                <div class="d-flex justify-content-between mb-2">
                  <div class="font-weight-bold">
                    <b>{{ menu.produk }}</b>
                  </div>
                  <div>{{ menu.harga }}</div>
                </div>
                <button @click="tambapesanan(menu)" class="btn rounded-4" style="background-color: #c78800; width: 95%">
                  <i class="bi bi-cart mx-4"></i>
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div class="cart shadow-lg">
    <h2><b>CART</b></h2>
    <div class="order-summary mt-4" style="width: 90%; height: 80%">
      <div v-for="(item, index) in orderItems" :key="index" class="card rounded-5 shadow mb-2">
        <div class="card-body" style="font-size: 120%">
          <b>
            <div class="container">
              <div class="row item-row align-items-center px-2">
                <div class="col-6 text-start">{{ item.produk }}</div>
                <div class="col-4 text-center">{{ item.quantity }}</div>
                <div class="col-2 text- end">
                  <button @click="hapusitem(index)" class="btn btn-trash" aria-label="Delete item">
                    <i class="bi bi-trash-fill"></i>
                  </button>
                </div>
              </div>
            </div>
          </b>
        </div>
      </div>
      <div class="card-body text-start">
        <hr />
        <h5 class="card-title" style="font-family: inter">
          TOTAL <span>: {{ totalbelanja }}</span>
        </h5>
        <button @click="tempatPesanan" class="btn chekout py-3 mt-3 rounded-5 order" id="or">
          <h4><b>ORDER</b></h4>
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
useHead({ title: 'MENU' });
definePageMeta({
  middleware: 'auth',
});
let user = useSupabaseUser();
const supabase = useSupabaseClient();
const router = useRouter();
const Menu = ref([]);
const orderItems = ref([]);
const totalbelanja = ref(0);
const keyword = ref('');

const getMenu = async () => {
  const { data, error } = await supabase.from('menu').select('*').ilike('produk', `%${keyword.value}%`);
  if (data) Menu.value = data;
};
const tambapesanan = (menu) => {
  const itemyangada = orderItems.value.find((item) => item.id === menu.id);
  if (itemyangada) {
    itemyangada.quantity++;
  } else {
    orderItems.value.push({ ...menu, quantity: 1 });
  }
  updateTotals();
};

const hapusitem = (index) => {
  const item = orderItems.value[index];
  if (item.quantity > 1) {
    item.quantity--;
  } else {
    orderItems.value.splice(index, 1);
  }
  updateTotals();
};

const updateTotals = () => {
  totalbelanja.value = orderItems.value.reduce((total, item) => total + item.harga * item.quantity, 0);
};
const tempatPesanan = async () => {
  const { error } = await supabase.from('statistik').insert([{ total: totalbelanja.value }]);
  if (!error) {
    localStorage.setItem('orderItems', JSON.stringify(orderItems.value));
    localStorage.setItem('totalbelanja', totalbelanja.value);
    orderItems.value = [];
    totalbelanja.value = 0;
    router.push('/struk');
  } else {
    alert('Order Gagal !!');
  }
};

onMounted(() => {
  getMenu();
});
</script>
<style scoped>
.cart {
  width: 30vw;
  height: 100vh;
  display: flex;
  position: fixed;
  top: 13%;
  right: 0%;
  background-color: white;
  padding: 10px;
}
#or {
  width: 100%;
  background-color: #c78800;
}
#ic {
  margin-top: 10%;
}
@media (min-width: 820px) {
  #c {
    display: none;
  }
}
@media (max-width: 820px) {
  .cart {
    right: -70%;
    text-align: center;
    width: 50vw;
    display: flex;
    position: fixed;
    top: 12%;
    font-size: 20px;
  }
  .card .rounded-5 .shadow .mb-2 {
    height: 10px;
  }
  .img {
    display: none;
  }
  .cart .container {
    height: 40px;
    font-size: small;
  }
  #or {
    background-color: rgb(146, 101, 2);
  }
  #ic {
    margin-top: 27%;
    text-align: center;
  }
}
</style>
