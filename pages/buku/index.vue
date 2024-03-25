<template>
    <div class="content">
        <div class="container-fluid">
            <div class="row" style="padding-top: 180px;">
                <div class="col-md-4 col-5" style="padding-left: 15%;">
                    <NuxtLink class="btn btn-lg rounded-5" to="/">
                        Isi Kunjungan
                    </NuxtLink>
                </div>
                <div class="col-lg-8 col-7" style="color: white; padding-left: 8%;">
                    <h1 class="m-0">Pencarian Buku</h1>
                </div>
            </div>
            <div class="row d-flex justify-content-center">
                <div class="col-10 pt-5">
                    <input type="text" class="form-control form-control-md rounded-5" name="cari-buku" id="cari-buku" placeholder="Cari Judul Buku🔍">
                </div>
            </div>
            <div class="row d-flex justify-content-center pt-2">
                <div class="col-6" style="color: white;">
                    <p class="m-0 pt-2">Menampilkan 4 dari 8</p>
                </div>
                <div class="col-2 text-end " style="color: white;">
                    <p class="m-0 pt-2">Kategori :</p>
                </div>
                <div class="col-2 ps-0">
                    <select name="kategori" id="kategori" class="form-control form-control-sm rounded-5 form-select">
                        <option value="" disabled selected>...</option>
                        <option value="">Novel</option>
                        <option value="">...</option>
                        <option value="">...</option>
                        <option value="">...</option>
                    </select>
                </div>
            </div>
            <div class="row" style="padding: 2% 0% 1% 5%;">
                <div class="col-3">
                    <NuxtLink to="/buku/rincian">
                        <img class="img-fluid" src="@/assets/img/Harry Potter 6.png" alt="">
                    </NuxtLink>
                </div>
                <div class="col-3">
                    <img class="img-fluid" src="@/assets/img/Bulan TereLiye.png" alt="">
                </div>
                <div class="col-3">
                    <img class="img-fluid" src="@/assets/img/Pulang Tere Liye.png" alt="">
                </div>
                <div class="col-3">
                    <img class="img-fluid" src="@/assets/img/Harry Potter 2.png" alt="">
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>

</script>

<style scoped>

.content {
    background-image: url('@/assets/img/bg-pencarianbuku.jpg');
    background-size: cover;
    width: 100%;
    height: 100vh;
    font-family: 'Jockey One';
}
.btn {
    background-color: #fffeee;
    /* padding: 0 30px;
    margin: 0 100px 0; */
}

img {
    width: 150px;
}
</style>