<template>
    <div class="container-fluid">
    <div class="row justify-content-center py-5">
        <div class="col-4 my-5 pb-1 px-4">
            <div class="card my-3 p-2 text-center rounded-5 bg-dark border-2 border-white" style="opacity: 80%;">
                <form  @submit.prevent="Login">
                    <div class="card-title mt-4 mb-4">
                        <i class="bi bi-person-circle " style="color:white; font-size: 90px;"></i>
                    </div>
                    <div class="mb-4 px-5 ">
                        <input  v-model="email"  type="email" class="form-control rounded-5" placeholder="Email .......">
                    </div>
                    <div class="mb-4 px-5">
                        <input  v-model="password" type="password" class="form-control rounded-5" placeholder="Password .......">
                    </div>
                    <em v-if="loading">sedang mengirim...</em>
                    <button type="submit" class="btn  mb-5 px-5 rounded-5" style="background-color:white; margin-left: 38%;">LOGIN</button>
                </form>
            </div>
        </div>
    </div>
</div>
</template>
<script setup>
definePageMeta({
    layout: 'login',
})
const supabase = useSupabaseClient()

const email = ref("")
const password = ref("")
const loading = ref(false)

const Login = async() => {
  loading.value = true
  const { data , error } = await supabase.auth.signInWithPassword({
    email: email.value,
    password: password.value,
  })
  if (data) {
    loading.value = false
    navigateTo("/")
  }
}
</script>
<style scoped>
.container-fluid{
    background-image: url(~/assets/img/bg-log.jpg);
    background-repeat: no-repeat;
    background-size: 100%;
    height: 100%;
}

</style>