<template>
  <div class="content">
    <div class="container-fluid">
      <div class="row">
        <div class="col layer">
          <form @submit.prevent="addData" autocomplete="off">
            <div class="row text-center fs-1 mb-4" style="color: white; font-family: 'Jockey One'; letter-spacing: 10px;">
              <p>Isi Kunjungan</p>
            </div>
            <div class="row mb-3">
              <input type="text" class="form-control form-control-lg rounded-4" id="nama" placeholder="Nama" required>
            </div>
            <div class="row mb-3">
              <select class="form-control form-control-lg form-select rounded-4" id="keanggotaan" required>
                <option value="" disabled selected>Keanggotaan</option>
                <option value="guru" >Guru</option>
                <option value="siswa" >Siswa</option>
                <option value="staf" >Staf</option>
                <option value="umum" >Umum</option>
              </select>
            </div>
            <div class="row">
              <div class="col p-0 mb-3">
                <select class="form-control form-control-lg form-select rounded-4" id="tingkat" required>
                  <option value="" disabled selected >Tingkat</option>
                  <option value="10">10</option>
                  <option value="11">11</option>
                  <option value="12">12</option>
                </select>
              </div>
              <div class="col mb-3">
                <select class="form-control form-control-lg form-select rounded-4" id="jurusan" required>
                  <option value="" disabled selected>Jurusan</option>
                  <option value="pplg" >PPLG</option>
                  <option value="tbsm" >TBSM</option>
                  <option value="tjkt" >TJKT</option>
                  <option value="toi" >TOI</option>
                  <option value="dkv" >DKV</option>
                </select>
              </div>
              <div class="col p-0 mb-3">
                <select class="form-control form-control-lg form-select rounded-4" id="kelas" required>
                  <option value="" disabled selected>Kelas</option>
                  <option value="1">1</option>
                  <option value="2">2</option>
                  <option value="3">3</option>
                  <option value="4">4</option>
                </select>
              </div>
            </div>
            <div class="row mb-3">
              <select class="form-control form-control-lg form-select rounded-4" id="keperluan" required>
                <option value="" disabled selected>Keperluan</option>
                <option value="berkunjung">Berkunjung</option>
                <option value="membaca">Membaca Buku</option>
                <option value="mengembalikan">Mengembalikan Buku</option>
                <option value="meminjam">Meminjam Buku</option>
              </select>
            </div>
            <div class="row float-end my-4">
              <NuxtLink id="btn" class="form-control rounded-4 text-decoration-none" to="/riwayat">Submit</NuxtLink>
              <!-- <input class="form-control rounded-4" style="width: 5rem;" id="btn" type="button" value="Submit"> -->
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>  
</template>

<script setup>

</script>

<style scoped>

.content {
  background-image: url("@/assets/img/bg-form.jpg");
  background-size: cover;
  max-width: 100%;
  height: 100vh;
}

.layer {
  background-image: linear-gradient(180deg, rgba(165, 160, 156, 0.5),rgba(72, 105, 133, 0.8),rgba(72, 105, 133, 0.8), rgba(165, 160, 156, 0.5));
  border-radius: 50px;
  margin: 10% 55% 0% 5%;
  padding: 2% 6%;
}

.form-control{
  background-color: #FFFEEE;
  font-family: 'Jockey One';
  color: rgba(0, 0, 0, 0.5);
  letter-spacing: 2px;
  font-size: 15px;
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