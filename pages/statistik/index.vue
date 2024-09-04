<template>
    <div class="container-fluid">
        <div class="row my-5 justify-content-around">
            <div class="col-5 mb-2">
                <div class="title-hari mx-5">
                    <h2>HARI INI</h2>
                </div>
                <div class="card rounded-5 mx-5">
                    <div class="card-body">
                        <h3>330000</h3>
                    </div>
                </div>
            </div>
            <div class="col-5 mb-2">
                <div class="title-bulan mx-5">
                    <h2>BULANAN INI</h2>
                </div>
                <div class="card rounded-5 mx-5">
                    <div class="card-body">
                        <h3>6300000</h3>
                    </div>
                </div>
            </div>
        </div>

        <div class="present text-center mx-4">
            <h4 class="mb-5 fw-bold">SEMUA OMZET</h4>
            <table class="table table-bordered">
                <thead>
                    <tr class="fw-bold">
                        <th style="width: 6%;">NO</th>
                        <th>TANGGAL</th>
                        <th>JUMLAH OMZET</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>1</td>
                        <td>20.8.2024</td>
                        <td>20000</td>
                    </tr>
                    <tr>
                        <td>2</td>
                        <td>20.8.2024</td>
                        <td>20000</td>
                    </tr><tr>
                        <td>3</td>
                        <td>20.8.2024</td>
                        <td>20000</td>
                    </tr><tr>
                        <td>4</td>
                        <td>20.8.2024</td>
                        <td>20000</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>
<script setup>
useHead({ title: "STATISTIK" })
</script>
<style scoped>
.card {
    background-color: #FF8000;
}

h3 {
    margin-top: 18px;
    font-size: 70px;
    margin-bottom: 18px;
}

@media (max-width: 820px) {
    h3 {
        margin-top: 5px;
        font-size: 40px;
        margin-bottom: 5px;
    }
}

.present {
    margin: 0 8%;
}
</style>