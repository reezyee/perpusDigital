<template>
    <div class="wrapper">
    <div class="content"></div>
        <div class="container-fluid">
            <div class="row" style="padding: 170px 0;">
                <div class="col-lg-4 col-12 d-flex flex-column align-items-center">
                    <img :src="buku?.cover" class="cover border" alt="cover" style="width: 250px;">
                    <div class="row ">
                        <NuxtLink to="/buku/" class="btn btn-lg rounded-5 mt-3" style="width: 10rem;">Kembali</NuxtLink>
                    </div>
                </div>
                <div class="col-lg-8 col-12">
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
                        <h6>{{ buku?.deskripsi }}</h6>
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
.wrapper{ 
    color: #fffeee;
    letter-spacing: 1.2px;
}

.content {
    background-image: url('@/assets/img/bg-rincianbuku.jpg');
    background-size: cover;
    background-repeat: no-repeat;
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
    font-family: 'Jockey One';
}
h1 {
    font-family: "Jockey One";
}
h4{
    font-family: "Jaldi"; 
    font-size: 30px;
}
h6 {
    font-family: "Jaldi";
    font-size: 20px;
    letter-spacing: 2px;
}
</style>