<template>
    <div class="wrapper p-5">
        <div class="content "></div>
        <div class="container-fluid">
            <div class="row d-flex align-items-center justify-content-center" style="padding-top: 150px;">
                <div class="col-lg-2 col-12">
                    <NuxtLink class="text-center" to="/">
                        <button class="btn btn-lg rounded-5">Isi Kunjungan</button>
                    </NuxtLink>
                </div>
                <div class="col-lg-8 text-center" style="color: white;">
                    <h1>
                        Riwayat <br> Kunjungan
                    </h1>
                </div>
                <div class="col-lg-2">
                    <NuxtLink class="text-center" to="/buku/">
                        <button class="btn btn-lg rounded-5">Cari Buku</button>
                    </NuxtLink>
                </div>
            </div>
            <div class="row" style="color: white;">
                <p>Menampilkan {{ visitors.length }} pengunjung</p>
                <div class="table table-responsive p-0">
                    <table class="table table-hover text-center">
                        <thead class="table-head">
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
                        <tbody class="table-body">
                            <tr v-for="(visitor, i) in visitors" :key="i">
                                <td>{{ i + 1 }}.</td>
                                <td>{{ visitor.tanggal }}</td>
                                <td>{{ visitor.waktu.split('.')[0] }}</td>
                                <td>{{ visitor.nama }}</td>
                                <td>{{ visitor.keanggotaan.nama }}</td>
                                <td>{{ visitor.kelas }}</td>
                                <td>{{ visitor.keperluan.nama }}</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
const supabase = useSupabaseClient()

const visitors = ref([])

async function getPengunjung() {
    const { data, error } = await supabase.from('pengunjung')
        .select(`*, keanggotaan(*), keperluan(*)`)
        .order('tanggal', { ascending: false })
    if (data) visitors.value = data
}

onMounted(() => {
    getPengunjung()
})
</script>

<style scoped>
.wrapper {
    width: 100%;
    height: 100%;
    background-repeat: no-repeat;
    background-size: auto;
    position: sticky;
    font-family: 'Jockey One';
}

.content {
    background-image: url('@/assets/img/BackgroundDaftarKunjungan.jpg');
    background-size: cover;
    background-repeat: no-repeat;
    font-family: "Jockey One";
    position: fixed;
    top: 0;
    background-position: center;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: -1;
}

.btn {
    background-color: #fffeee;
    width: 10rem;
}

/* .lk{
    display: flex;
    align-items: center;
} */

.table {
    --bs-table-bg: none;
    --bs-table-color: white;
    border-top-left-radius: 25px;
    border-top-right-radius: 25px;
    letter-spacing: 2px;
}

.table-head {
    background-color: #305075;
}

.table-body {
    background-color: #7395BA;
    border: 1px solid;
}

td {
    padding: 5px 0px;
    border: 1px solid;
}

@media (max-width: 900px) {

    /* .lk {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    } */
    .lk {
        display: flex;
        justify-content: center;
        align-items: center;
    }
}
</style>