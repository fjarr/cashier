<template>
  <div class="bg">
    <div class="container-fluid">
      <div class="row mt-1">
        <div class="col-12 col-lg-8 col-md-8 col-sm-12 my-4">
          <form @submit.prevent="getMenu" class="d-flex mx-5 mb-4 px-5" id="ic">
            <input v-model="keyword" class="form-control rounded-pill " type="search"
              placeholder="Mau Beli Apaa ...........?" aria-label="Search" :disabled="loading" />
          </form>
          <div v-if="loading">Loading...</div>
          <div class="row">
            <div class="col-12 col-lg-4 col-md-6 col-sm-12 mb-4" v-for="(menu, i) in Menu" :key="i">
              <div class="card shadow rounded-4">
                <div class="img p-2">
                  <img :src="menu.cover" class="card-img-top rounded-3" alt="cover"
                    style="height: 150px; object-fit: cover" />
                </div>
                <div class="card-body">
                  <div class="d-flex justify-content-between mb-2">
                    <div class="font-weight-bold">
                      <b>{{ menu.produk }}</b>
                    </div>
                    <div>{{ menu.harga }}</div>
                  </div>
                  <button @click="tambapesanan(menu)" class="btn rounded-4"
                    style="background-color: #c78800; width: 95%">
                    <i class="bi bi-cart mx-4"></i>
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="cart">
      <div class="order-summary mt-4" style="width: 90%; height: auto">
        <div class="scrollable-container">
          <div v-for="(item, index) in orderItems" :key="index" class="card rounded-5 shadow mb-2">
            <div class="card-body">
              <div class="container">
                <div class="row item-row align-items-center px-1">
                  <div class="col-5 text-center">{{ item.produk }}</div>
                  <div class="col-4 text-center">{{ item.quantity }}</div>
                  <div class="col-3 text-center">
                    <button @click="hapusitem(index)" class="btn btn-trash" aria-label="Delete item">
                      <i class="bi bi-trash-fill"></i>
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="card-body" id="cb">
          <div class="row text-center">
            <div class="col-12 d-none d-lg-block">
              <h5 class="card-title"  id="tb">
                ITEMS <span>: {{ orderItems.length }}</span>
              </h5>
              <h5 class="card-title my-3">
                TOTAL <span>: {{ totalbelanja }}</span>
              </h5>
              <div class="text-center mt-2">
                <button @click="tempatPesanan" class="btn chekout rounded-5 order py-4" id="or">
                  <b>ORDER</b>
                </button>
              </div>
            </div>
            <div class="col-12 d-lg-none">
              <div class="row text-center">
                <div class="col mt-2">
                  <h5 class="card-title">ITEMS <span> : <br> {{ orderItems.length }}</span></h5>
                </div>
                <div class="col mt-2">
                  <h5 class="card-title">TOTAL <span>: <br>{{ totalbelanja }}</span></h5>
                </div>
                <div class="col">
                  <div class="co">
                    <button @click="tempatPesanan" class="btn chekout rounded-5 order" id="or">
                      <b>ORDER</b>
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
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
const cartVisible = ref(false);
const loading = ref(false);

const getMenu = async () => {
  loading.value = true;
  const { data, error } = await supabase.from('menu').select('*').ilike('produk', `%${keyword.value}%`);
  loading.value = false;
  if (data) {
    Menu.value = data;
  } else {
    alert('Error fetching menu items');
  }
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
.bg {
  background-image: url(~/assets/img/bgm2.png);
}

.cart {
  width: 30vw;
  display: flex;
  position: fixed;
  top: 19%;
  right: 0;
  padding: 20px;
  background-color: transparent;
  border-radius: 15px;
  transition: right 0.3s;
  z-index: 1000;
}

.cart.hidden {
  display: none;
}

.scrollable-container {
  max-height: 360px;
  overflow-y: auto;
}

#or {
  width: 100%;
  background-color: #c78800;
  text-align: center;
  border-radius: 5px;
}

#tb {
  display: none;
}
@media (max-width: 520px) {
  .cart {
    width: 100vw;
    text-align: center;
    display: flex;
    position: sticky;
    bottom: 0%;
    font-size: 1rem;
    margin: auto;
    padding: 2px;
    background-color: white;
  }

  .img {
    display: none;
  }

  .scrollable-container {
    display: none;
  }

  h5 {
    font-size: x-small;
  }

  b {
    font-size: small;
  }
  .co{
    margin-bottom: 20px;

  }
  #or {
    width: 80%;
    height: 100%;
  }
}
</style>
