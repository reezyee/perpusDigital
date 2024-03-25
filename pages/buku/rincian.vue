<template>
    <div class="content">
        <div class="container-fluid">
            <div class="row d-flex justify-content-center flex-md-wrap" style="padding-top: 180px;">
                <div class="col-3">
                    <img class="img-fluid" src="@/assets/img/Harry Potter 6.png" alt="">
                    <div class="row">
                        <NuxtLink to="/buku/" class="btn btn-lg rounded-5">Kembali</NuxtLink>
                    </div>
                </div>
                <div class="col-8">
                    <div class="row">
                        <h1>Harry Potter and the Half-Blood Prince</h1>
                    </div>
                    <div class="row">
                        <p>Pengarang : J.K Rowling</p>
                        <p>Tahun Terbit : 16 Juli 2005</p>
                        <p>Genre : Novel, Fiksi</p>
                    </div>
                    <div class="row">
                        <p>   Harry Potter and the Half-Blood Prince adalah film keenam dari seri film Harry Potter yang didasarkan pada novel berjudul sama karya J. K. Rowling. Film ini disutradarai oleh David Yates yang juga menyutradarai film kelima, The Order of the Phoenix.</p>
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
</style>