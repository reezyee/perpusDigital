<template>
    <div class="wrapper p-5">
        <div class="content "></div>
        <div class="container-fluid">
            <div class="row d-flex align-items-center justify-content-center" style="padding-top: 145px;">
                <div class="col-lg-2 col-md-3 col-8">
                    <NuxtLink class="text-center" to="/">
                        <button class="btn btn-lg rounded-5">Isi Kunjungan</button>
                    </NuxtLink>
                </div>
                <div class="col-lg-7 col-md-3 col text-center text-white" >
                    <h1>
                        Riwayat <br> Kunjungan
                    </h1>
                </div>
                <div class="col-lg-2 col-md-3 col-8">
                    <NuxtLink class="text-center" to="/buku/">
                        <button class="btn btn-lg rounded-5">Cari Buku</button>
                    </NuxtLink>
                </div>
                <form @submit.prevent="getVisitors" class="row py-4 d-flex justify-content-center">
                    <div class="col-lg-2 col-md-3 col-8">
                        <p class="m-0 text-white text-center">Menampilkan {{ visitorFiltered.length }} dari {{ amountVisitors }} pengunjung</p>
                    </div>
                    <div class="col-lg-7 col-md-6 pt-1">
                        <input v-model="keyword" type="search" class="form-control form-control-md rounded-5" name="cari-buku" id="cari-buku" placeholder="Cari Nama Pengunjung" autocomplete="off">
                    </div>
                    <!-- <div class="row my-3 d-flex justify-content-center ps-0"> -->
                        <!-- <p class="col-2 text-white m-0 text-end mt-2" style="letter-spacing: 3px;">kategori :</p> -->
                        <div class="col-lg-3 col-md-3 pt-1 ">
                            <select v-model="keyword" name="kategori" id="kategori" class="form-control form-control-sm rounded-5 form-select">
                                <option value="" disabled selected>Kategori?</option>
                                <option v-for="(category, i) in categories" :key="i" :value="category.nama">{{ category.nama }}</option>
                            </select>
                        </div>
                    <!-- </div> -->
                </form>
            </div>
            <div class="row text-white">
                <!-- <table class="table"> -->
                    <div class="table table-head table-responsive">
                        <table class="table text-center">
                            <thead>
                                <tr>
                                    <th style="width: 50px;">No</th>
                                    <th style="width: 120px;">Tanggal</th>
                                    <th style="width: 120px;">Jam</th>
                                    <th style="width: 150px;">Nama</th>
                                    <th style="width: 90px;">Kategori</th>
                                    <th style="width: 140px;">Kelas</th>
                                    <th style="width: 260px;">Keperluan</th>
                                </tr>
                            </thead>
                        </table>
                    </div>
                    <div class="table-responsive table-body ">
                        <table class="table table-hover text-center">
                            <tbody>
                                <tr v-for="(visitor, i) in visitorFiltered" :key="i">
                                    <td style="width: 20px;">{{ i + 1 }}.</td>
                                    <td style="width: 50px;">{{ visitor.tanggal }}</td>
                                    <td style="width: 50px;">{{ visitor.waktu.split('.')[0] }}</td>
                                    <td style="width: 50px;">{{ visitor.nama }}</td>
                                    <td style="width: 50px;">{{ visitor.keanggotaan.nama }}</td>
                                    <td style="width: 50px;">{{ visitor.kelas }}</td>
                                    <td style="width: 50px;">{{ visitor.keperluan.nama }}</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                <!-- </table> -->
            </div>
        </div>
    </div>
</template>

<script setup>
const supabase = useSupabaseClient()

const visitors = ref([])
const keyword = ref('')
const categories =ref([])
const amountVisitors = ref(0)

async function getVisitors() {
    const { data, error } = await supabase.from('pengunjung')
        .select(`*, keanggotaan(*), keperluan(*)`)
        .ilike('nama', `%${keyword.value}%`)
        .order('id', { ascending: false })
    if (data) visitors.value = data
}

async function getCategory(){
    const{data, error} = await supabase.from('keanggotaan')
    .select('*')
    if(data) categories.value = data
}

const visitorFiltered = computed (() => {
    return visitors.value.filter((b) => {
        return (
            b.nama?.toLowerCase().includes(keyword.value?.toLowerCase()) ||
            b.keanggotaan?.nama.toLowerCase().includes(keyword.value?.toLowerCase())
        )
    })
}) 

async function getAmountVisitors()
{
    const {data , count} = await supabase.from('pengunjung')
    .select('*', { count: "exact"})
    if (data) amountVisitors.value = count
}

onMounted(() => {
    getVisitors()
    getCategory()
    getAmountVisitors()
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

.form-control{
    background-color: #fffeee;
}

.table {
    --bs-table-bg: none;
    --bs-table-color: white;
    border-top-left-radius: 25px;
    border-top-right-radius: 25px;
    letter-spacing: 2px;
    margin: 0;
    
}

.table-head {
    background-color: #305075;
    /* width: 100%; */
    margin: 0;
    padding: 0;
}

.table-body {
    background-color: #7395BA;
    border: 1px solid;
    max-height: 210px;
    /* width: 100%; */
    padding: 0;
}

/* th{
    border: 1px solid;

} */
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
