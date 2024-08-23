<template>
  <div class="container-fluid">
    <div class="row">
      <!-- Menu items -->
      <div class="col-12 col-lg-8 col-md-8 col-sm-12 my-4">
        <div class="row">
          <div class="col-12 col-lg-4 col-md-6 col-sm-12 mb-4" v-for="(menu, i) in Menu" :key="i">
            <div class="card shadow rounded-4">
              <!-- Image section -->
              <div class="img p-2">
                <img :src="menu.cover" class="card-img-top rounded-3" alt="cover" style="height: 150px; object-fit: cover;">
              </div>
              <!-- Card body section -->
              <div class="card-body">
                <div class="d-flex justify-content-between mb-2">
                  <div class="font-weight-bold"><b>{{ menu.produk }}</b></div>
                  <div>{{ menu.harga }}</div>
                </div>
                <button @click="addToOrder(menu)" class="btn rounded-4" style="background-color: #c78800; width: 95%;">
                  <i class="bi bi-cart mx-4"></i>
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
      <!-- Order section -->
      <div class="col-12 col-lg-4 d-flex justify-content-end align-items-start my-4 shadow">
        <div  class="order-summary mt-4">
          <div v-for="(item, index) in orderItems" :key="index" class="card rounded-5 shadow mb-2">
            <div  class="card-body" style="font-size: 120%;">
              <b>
                <div class="container ">
                  <div  class="row item-row align-items-center">
                    <div class="col-md-6">{{ item.produk }}</div>
                    <div class="col-md-4 text-right">{{ item.quantity }}</div>
                    <div class="col-md-2 text-center">
                      <button @click="removeFromOrder(index)" class="btn btn-trash" aria-label="Delete item">
                        <i class="bi bi-trash-fill"></i>
                      </button>
                    </div>
                  </div>
                </div>
              </b>
            </div>
          </div>
          <div class="card-body">
            <hr>
            <h5 class="card-title">TOTAL PRICE <span>: {{ totalPrice }}</span></h5>
            <button @click="placeOrder" class="btn chekout ms-3 py-3 mt-3 rounded-5" style="width: 90%; background-color: #c78800;">
              <h4><b>ORDER</b></h4>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

  
  <style scoped>
  .order-summary {
    position: sticky;
    top: 0;
    width: 100%;
    max-width: 400px;
  }
  
  hr {
    height: 5px;
  }
  </style>
  
  <script setup>
useHead({ title: "MENU" })
const supabase = useSupabaseClient()
const Menu = ref([])
const orderItems = ref([])
const totalPrice = ref(0)

const getMenu = async () => {
  const { data, error } = await supabase.from('menu').select('*')
  if (data) Menu.value = data
}

const addToOrder = (menu) => {
  const existingItem = orderItems.value.find(item => item.id === menu.id)
  if (existingItem) {
    existingItem.quantity++
  } else {
    orderItems.value.push({ ...menu, quantity: 1 })
  }
  updateTotals()
}

const removeFromOrder = (index) => {
  const item = orderItems.value[index]
  if (item.quantity > 1) {
    item.quantity--
  } else {
    orderItems.value.splice(index, 1)
  }
  updateTotals()
}
const updateTotals = () => {
  totalPrice.value = orderItems.value.reduce((total, item) => total + item.harga * item.quantity, 0)
}

const placeOrder = async () => {
  const { error } = await supabase.from('statistik').insert([{ total: totalPrice.value }])
  if (!error) {
    orderItems.value = []
    totalPrice.value = 0
    return navigateTo('/struk')
  } else {
    console.error(error)
    alert('Order Gagal !!')
  }
}

onMounted(() => {
  getMenu()
})
</script>
