<template>
    <div class="wrapper">
    <div class="content"></div>
        <div class="container-fluid">
            <div class="row" style="padding-top: 190px;">
                <div class="col-md-4 col-5" style="padding-left: 15%;">
                    <NuxtLink class="btn btn-lg rounded-5" to="/">
                        Isi Kunjungan
                    </NuxtLink>
                </div>
                <div class="col-lg-8 col-7" style="color: white; padding-left: 8%;">
                    <h1 class="m-0">Pencarian Buku</h1>
                </div>
            </div>
                <form @submit.prevent="getBooks" class="row pt-5 d-flex justify-content-center">
                    <div class="col-lg-10">
                        <input v-model="keyword" type="search" class="form-control form-control-md rounded-5" name="cari-buku" id="cari-buku" placeholder="Cari Judul Buku🔍" autocomplete="off">
                    </div>
                    <div class="row my-3 d-flex justify-content-center ps-0">
                        <p class="col-6 m-0 pt-2 text-white" style="letter-spacing: 3px;">Menampilkan {{ bookFiltered.length }} dari {{ jumlahBuku }} buku</p>
                        <!-- <p class="col-2 text-white m-0 text-end mt-2" style="letter-spacing: 3px;">kategori :</p> -->
                        <div class="col-4   ">
                            <select v-model="keyword" name="kategori" id="kategori" class="form-control form-control-sm rounded-5 form-select" @change="getBooks">
                                <option value="" selected disabled>Kategori?</option>
                                <option v-for="(kategori, i) in kategories" :key="i" :value="kategori.nama">{{ kategori.nama }}</option>
                            </select>
                        </div>
                    </div>
                </form>
                <div class="row">
                <div v-for="(book, i) in bookFiltered" :key="i" class="col">
                    <div class="card cb col-lg-2 col-md-4 col-sm-4 col-6">
                        <div class="card-body">
                            <NuxtLink :to="`/buku/${book.id}`" style="text-decoration:none">
                                <img :src="book.cover" class="cover border" :alt="book.judul">
                            </NuxtLink>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
const supabase = useSupabaseClient()

const books = ref([])
const kategories = ref([])
const keyword = ref('')
// const kategori = ref(null)
const jumlahBuku = ref(0)

async function getBooks() {
    const {data, error} = await supabase.from('buku')
    .select(`*, kategori(*)`)
    .ilike('judul', `%${keyword.value}%`)
    // if (kategori.value) query = query.eq('kategori', kategori.value)
    // const {data , error} = await query
    .order('id')
    if (error) throw error
    if (data) {
    books.value = data; 
        data.forEach(book => {
            const { data } = supabase.storage.from('cover').getPublicUrl(book.cover)
            if (data) {
                book.cover = data.publicUrl
            }
        })
    }
}

async function getKategori(){
    const{data, error} = await supabase.from('kategori_buku')
    .select('*')
    if(data) kategories.value = data
}

const bookFiltered = computed (() => {
    return books.value.filter((b) => {
        return (
            b.judul?.toLowerCase().includes(keyword.value?.toLowerCase()) ||
            b.kategori?.nama.toLowerCase().includes(keyword.value?.toLowerCase())
        )
    })
}) 

async function getJumlahBuku()
{
    const {data , count} = await supabase.from('buku')
    .select('*', { count: "exact"})
    if (data) jumlahBuku.value = count
}


onMounted(() => {
    getBooks()
    getKategori()
    getJumlahBuku()
})
</script>

<style scoped>
.wrapper{
    font-family: 'Jockey One';
}
.content {
    background-image: url('@/assets/img/bg-pencarianbuku.jpg');
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
.btn  {
    background-color: #fffeee;
    /* padding: 0 30px;
    margin: 0 100px 0; */
}

.form-control{
    background-color: #fffeee;
}

img {
    width: 150px;
}

.cb {
    background-color: rgba(217, 217, 217, 0.80);
    border: 0;
    height: 250px;
    width: 180px;
    margin: 5px 5px;
}
</style>