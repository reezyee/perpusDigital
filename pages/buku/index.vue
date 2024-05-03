<template>
    <div class="content">
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
            <!-- <div class="d-flex justify-content-center"> -->
                <form @submit.prevent="getBooks" class="row pt-5 d-flex justify-content-center">
                    <div class="col-lg-10">
                        <input v-model="keyword" type="text" class="form-control form-control-md rounded-5" name="cari-buku" id="cari-buku" placeholder="Cari Judul Buku🔍" autocomplete="off">
                    </div>
                    <!-- <div class="row ps-0 float-end"> -->
                    <p class="col-6 m-0 pt-2 text-white mt-2">Menampilkan {{ books.length }} buku</p>
                    <div class="col-4 my-3 d-flex flex-direction-col ps-0">
                        <p class="col-3 text-white m-0">kategori :</p>
                        <select v-model="keyword" name="kategori" id="kategori" class="form-control form-control-sm rounded-5 form-select">
                            <option value="" disabled selected>Kategori?</option>
                            <option v-for="(kategories, i) in kategories" :key="i" :value="kategories.id">{{ kategories.nama }}</option>
                        </select>
                    </div>
                    <!-- </div> -->
                </form>
            <!-- </div> -->
            <!-- <div class="row d-flex justify-content-center pt-2">
                
            </div> -->
            <div class="row">
                <div v-for="(book, i) in validationBook" :key="i" class="col">
                    <div class="card">
                        <div class="card-body">
                            <img :src="book.coverUrl.publicUrl" class="cover" alt="cover">
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
const keyword = ref('')
const kategories = ref('')

async function getBooks() {
    const {data, error} = await supabase.from('buku')
    .select(`*, kategori_buku ( * )`)
    .ilike('judul', `%${keyword.value}%`)
    if (error) throw error
    if (data) {
        books.value = data
        data.forEach(book => {
            const { data } = supabase.storage.from('cover').getPublicUrl(book.cover)
            if (data) {
                book.coverUrl = data
            }
        })
    }
}

async function getKategori(){
    const{data, error} = await supabase.from('kategori_buku')
    .select('*')
    if(data) kategories.value = data
}

const validationBook = computed (() => {
    return books.value.filter((b) => {
        return (
            b.judul?.toLowerCase().includes(keyword.value?.toLowerCase()) ||
            b.kategori?.nama.toLowerCase().includes(keyword.value?.toLowerCase())
    )
    })
}) 


onMounted(() => {
    getBooks()
    getKategori()
})
</script>

<style scoped>

.content {
    background-image: url('@/assets/img/bg-pencarianbuku.jpg');
    background-size: cover;
    width: 100%;
    /* height: 100vh; */
    font-family: 'Jockey One';
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
</style>