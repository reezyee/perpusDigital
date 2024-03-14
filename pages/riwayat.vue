<template>
    <div class="content">
        <div class="container-fluid">
            <div class="row pt-5">
                <div class="col fe">
                    <NuxtLink class="btn btn-lg rounded-5" to="/">
                        Isi Kunjungan
                    </NuxtLink>
                </div>
                <div class="col fe text-center" style="color: white;">
                    <h1>
                        Riwayat <br> Kunjungan
                    </h1>
                </div>
                <div class="col fe">
                    <NuxtLink class="btn btn-lg rounded-5">
                        Cari Buku
                    </NuxtLink>
                </div>
            </div>
            <div class="row">
                <p>Menampilkan 5 dari 10</p>
                <div class="table table-responsive">
                    <table class="table table-hover">
                        <thead>
                            <tr>
                                <th>No</th>
                                <th>Tanggal</th>
                                <th>Jam</th>
                                <th>Nama</th>
                                <th>Kategori</th>
                                <th>Kelas</th>
                                <th>Keperluan</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>1</td>
                                <td>2</td>
                                <td>3</td>
                                <td>4</td>
                                <td>5</td>
                                <td>6</td>
                                <td>7</td>
                            </tr>
                            <tr>
                                <td>1</td>
                                <td>2</td>
                                <td>3</td>
                                <td>4</td>
                                <td>5</td>
                                <td>6</td>
                                <td>7</td>
                            </tr>
                            <tr>
                                <td>1</td>
                                <td>2</td>
                                <td>3</td>
                                <td>4</td>
                                <td>5</td>
                                <td>6</td>
                                <td>7</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>

</script>

<style scoped>
.content {
    background-image: url('@/assets/img/BackgroundDaftarKunjungan.jpg');
    background-size: cover;
    width: 100%;
    height: 100vh;
}

.btn {
    background-color: #fffeee;
    padding: 0 30px;
    margin: 0 100px 0;

}
.fe {
    margin: 150px 0 0 0;
}

</style>