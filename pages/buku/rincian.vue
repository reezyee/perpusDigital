<template>
    <div class="content">
        <div class="container-fluid">
            <div class="row d-flex justify-content-center flex-md-wrap" style="padding-top: 190px;">
                <div class="col-3">
                    <img class="row img-fluid" src="@/assets/img/Harry Potter 6.png" alt="" style="width: 250px;">
                    <div class="row">
                        <NuxtLink to="/buku/" class="btn btn-lg rounded-5" style="width: 10rem;">Kembali</NuxtLink>
                    </div>
                </div>
                <div class="col-8">
                    <div class="row">
                        <h1>Harry Potter and the Half-Blood Prince</h1>
                    </div>
                    <div class="row">
                        <h4>Pengarang : J.K Rowling</h4>
                        <h4>Tahun Terbit : 16 Juli 2005</h4>
                        <h4>Genre : Novel, Fiksi</h4>
                    </div>
                    <div class="row">
                        <h6>Harry Potter and the Half-Blood Prince adalah film keenam dari seri film Harry Potter yang didasarkan pada novel berjudul sama karya J. K. Rowling. Film ini disutradarai oleh David Yates yang juga menyutradarai film kelima, The Order of the Phoenix.</h6>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>

</script>

<style scoped>
.content {
    background-image: url('@/assets/img/bg-rincianbuku.jpg');
    background-size: cover;
    width: 100%;
    height: 100vh;
    font-family: 'Jockey One';
    color: white;
}
.btn {
    background-color: #fffeee;
}
/* .rincicard {
    background-color: #fffeee00;
} */
</style>