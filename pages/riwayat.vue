<template>
    <div class="content p-5">
        <div class="container-fluid">
            <div class="row lk" style="padding-top: 150px;">
                <div class="col">
                    <NuxtLink class="btn btn-lg rounded-5" to="/">
                        Isi Kunjungan
                    </NuxtLink>
                </div>
                <div class="col text-center" style="color: white;">
                    <h1>
                        Riwayat <br> Kunjungan
                    </h1>
                </div>
                <div class="col">
                    <NuxtLink class="btn btn-lg rounded-5" to="/buku/">
                        Cari Buku
                    </NuxtLink>
                </div>
            </div>
            <div class="row" style="color: white;">
                <p>Menampilkan {{  visitors.length }} pengunjung</p>
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
                                <td>{{ i+1 }}.</td>
                                <td>{{ visitor.tanggal }}</td>
                                <td>{{ visitor.waktu.split('.')[0] }}</td>
                                <td>{{  visitor.nama }}</td>
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
    const {data, error} = await supabase.from('pengunjung')
    .select(`*, keanggotaan(*), keperluan(*)`)
    if (data) visitors.value = data
}

onMounted(() => {
    getPengunjung()
})
</script>

<style scoped>

.content {
    background-image: url('@/assets/img/BackgroundDaftarKunjungan.jpg');
    background-size: cover;
    width: 100%;
    /* height: 100vh; */
    font-family: "Jockey One";
}
.btn {
    background-color: #fffeee;
    margin-left: 100px;
}

.lk{
    display: flex;
    align-items: center;
}

.table{
    --bs-table-bg : none;
    --bs-table-color: white;
    border-top-left-radius: 25px;
    border-top-right-radius: 25px;
    letter-spacing: 2px;
}
.table-head{
    background-color: #305075;
}
.table-body{
    background-color: #7395BA;
    border: 1px solid ;
}
td {
    padding: 5px 0px;
    border: 1px solid ;
}

@media (max-width: 675px) {
    .lk {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
    .btn {
    margin-left: 200px;
}
}

@media (max-width: 500px) {
    .lk {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
    .btn {
    margin-left: 80px;
}
}
</style>