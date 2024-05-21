<template>
    <div class="content">
        <div class="container-fluid">
            <div class="row d-flex justify-content-center flex-md-wrap" style="padding-top: 190px;">
                <div class="col-3">
                    <img :src="buku?.cover" class="cover border" alt="cover" style="width: 200px;">
                    <div class="row">
                        <NuxtLink to="/buku/" class="btn btn-lg rounded-5" style="width: 10rem;">Kembali</NuxtLink>
                    </div>
                </div>
                <div class="col-8">
                    <div class="row">
                        <h1>{{ buku?.judul }}</h1>
                    </div>
                    <div class="row">
                        <h4>Pengarang : {{ buku?.penulis }}</h4>
                        <h4>Penerbit : {{ buku?.penerbit }}</h4>
                        <h4>Tahun Terbit : {{ buku?.tahun_terbit }}</h4>
                        <h4>Genre : {{ buku?.genre }}</h4>
                    </div>
                    <div class="row">
                        <h6>{{ buku?.deskripsi }}.</h6>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
const supabase = useSupabaseClient()

const route = useRoute()
const buku = ref()

const getBookById = async () => {
    const { data, error } = await supabase.from('buku')
    .select(`*, kategori_buku(*)`)
    .eq('id', route.params.id)
    .maybeSingle()
    if (error) throw error
    if (data) {
        const { data: url } = supabase.storage.from('cover').getPublicUrl(data.cover)
        if (url) {
            data.cover = url.publicUrl
        }
        buku.value = data
    }
}

onMounted(() => {
    getBookById()
})
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