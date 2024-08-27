<template>
    <div class="container-fluid d-flex justify-content-center mt-5">
        <table class="table table-bordered" style="width:85%;">
            <thead>
                <tr class="fw-bold">
                    <td>NAMA BARANG</td>
                    <td style="width: 6%;">JUMLAH</td>
                    <td>HARGA BARANG</td>
                    <td>TOTAL HARGA</td>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>baso</td>
                    <td>2</td>
                    <td>4000</td>
                    <td>8000</td>
                </tr>
            </tbody>
        </table>
    </div>
    <div class="total  d-flex justify-content-center mt-5">
        <table class="text-center" style="width:85%; align-items: center;">
            <tr class="fw-bold">
                <td>TOTAL ALL</td>
                <td>INPUT UANG </td>
                <td>TOTAL KEMBALIAN</td>
            </tr>
            <tr>
                <td>8000</td>
                <td style="width: 20%; align-items: center;"> 
                <input class="form-control rounded-5 " type="search" placeholder="uang mu berapa?"  >
                </td>
                <td>2000</td>
            </tr>
        </table>
    </div>
</template>