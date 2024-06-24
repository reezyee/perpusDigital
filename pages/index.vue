<template>
  <div class="wrapper">
  <div class="content"></div>
    <div class="container-fluid">
      <div class="row">
        <div class="col layer">
          <form @submit.prevent="tambahData" autocomplete="off">
            <div class="row text-center fs-1 mb-4" style="color: white; font-family: 'Jockey One'; letter-spacing: 10px;">
              <p>Isi Kunjungan</p>
            </div>
            <div class="row mb-3">
              <input v-model.trim="nama" type="text" class="form-control form-control-lg rounded-4" id="nama" placeholder="Nama" required>
            </div>
            <div class="row mb-3">
              <select v-model="keanggotaan" @change="resetKelas" class="form-control form-control-lg form-select rounded-4" id="keanggotaan" required>
                <option value="" disabled selected>Keanggotaan</option>
                <option v-for="(keanggotaan, i) in members" :key="i" :value="keanggotaan.id">{{ keanggotaan.nama }}</option>
              </select>
            </div>
            <div v-if="keanggotaan == '2'" class="row">
              <div class="col p-0 mb-3">
                <select v-model="tingkat" class="form-control form-control-lg form-select rounded-4" id="tingkat" required>
                  <option value="" disabled selected >Tingkat</option>
                  <option value="10">10</option>
                  <option value="11">11</option>
                  <option value="12">12</option>
                </select>
              </div>
              <div class="col mb-3">
                <select v-model="jurusan" class="form-control form-control-lg form-select rounded-4" id="jurusan" required @change="selectJurusan">
                  <option value="" disabled selected>Jurusan</option>
                  <option value="PPLG">PPLG</option>
                  <option value="TBSM">TBSM</option>
                  <option value="TJKT">TJKT</option>
                  <option value="TOI">TOI</option>
                  <option value="DKV">DKV</option>
                </select>
              </div>
              <div class="col p-0 mb-3">
                <select v-model="kelas" :disabled="!jurusan || jurusan=='TOI'" class="form-control form-control-lg form-select rounded-4" id="kelas" required>
                  <option value="" disabled selected>Kelas</option>
                  <option value="1">1</option>
                  <option value="2">2</option>
                  <option v-if="!(jurusan=='DKV')" value="3">3</option>
                  <option v-if="!(jurusan=='DKV')" value="4">4</option>
                </select>
              </div>
            </div>
            <div class="row mb-3">
              <select v-model="keperluan" class="form-control form-control-lg form-select rounded-4" id="keperluan" required>
                <option value="" disabled selected>Keperluan</option>
                <option v-for="(keperluan, i) in objectives" :key="i" :value="keperluan.id">{{ keperluan.nama }}</option>
              </select>
            </div>
            <div class="row float-end my-4">
              <input class="form-control form-control-lg rounded-5" id="btn" type="submit" value="Submit">
              <!-- <input class="form-control rounded-4" style="width: 5rem;" id="btn" type="button" value="Submit"> -->
            </div>
          </form>
        </div>
      </div>
      <NuxtLink class="from-control form-control-lg rounded-5 text-decoration-none text-center mt-2 fs-3 float-end unvisible" to="/riwayat">
        >
      </NuxtLink>
    </div>
  </div>  
</template>

<script setup>
const supabase= useSupabaseClient()

const members = ref([])
const objectives = ref([])
const nama = ref('')
const keanggotaan = ref('')
const tingkat = ref('')
const jurusan = ref('')
const kelas = ref('')
const keperluan = ref('')
const kelasLengkap = ref('')

async function tambahData(){
  kelasLengkap.value = `${tingkat.value} ${jurusan.value} ${kelas.value}`
  const { error } = await supabase.from('pengunjung')
  .insert([{
    keanggotaan: keanggotaan.value,
    kelas: kelasLengkap.value,
    nama: nama.value,
    keperluan: keperluan.value
  }])
  if (error) throw error
  else navigateTo('/riwayat')
}

async function getKeanggotaan(){
  const{data, error} = await supabase.from('keanggotaan')
  .select('*')
  if(data) members.value = data
}

async function getKeperluan(){
  const{data, error} = await supabase.from('keperluan')
  .select('*')
  if(data) objectives.value = data
}

function resetKelas(e){
    if(e.target.value != '2'){
        kelas.value= ''
        tingkat.value= ''
        jurusan.value= ''
    }
}

const selectJurusan = () => {
  if (jurusan.value == 'TOI') {
    kelas.value = ''
  }
}

onMounted(() => {
  getKeanggotaan()
  getKeperluan()
})
</script>

<style scoped>
.wrapper{
  font-family: 'Jockey One';
}
.content {
  background-image: url("@/assets/img/bg-form.jpg");
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


.layer {
  background-image: linear-gradient(180deg, rgba(165, 160, 156, 0.5),rgba(72, 105, 133, 0.8),rgba(72, 105, 133, 0.8), rgba(165, 160, 156, 0.5));
  border-radius: 50px;
  margin: 10% 55% 0% 5%;
  padding: 2% 6%;
  width: 20rem;
}

.form-control{
  background-color: #FFFEEE;
  font-family: 'Jockey One';
  color: rgba(0, 0, 0, 0.7);
  letter-spacing: 2px;
  font-size: 20px;
}

.unvisible{
  color: #fffeee07;
}
/* #nama , #keanggotaan, #keperluan{
  width: 25rem;
} */

#btn{
  background-color: #0C5EA1;
  border: none;
  color: white;
}
@media (max-width: 900px) {
  .layer {
    margin: 30% 10% 1% 10%;
  }
}
@media (max-width: 600px) {
  .layer {
    margin: 40% 5% 1% 5%;
  }
}
@media (max-width: 460px) {
  .layer {
    margin: 55% 5% 1% 5%;
  }
}
</style>