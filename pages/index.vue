<template>
  <div class="content">
    <div class="container-fluid">
      <div class="row">
        <div class="col p-5 p">
          <form @submit.prevent="" autocomplete="none" class="layer">
            <div class="row text-center mb-4" style="color: white;">
              <h3>Isi Kujungan</h3>
            </div>
            <div class="row mb-3">
              <input type="text" class="form-control form-control-lg rounded-4" placeholder="Nama" required>
            </div>
            <div class="row mb-3">
              <select class="form-control form-control-lg rounded-4" id="keanggotaan" required>
                <option value="" disabled>Keanggotaan</option>
                <option value="" >Guru</option>
                <option value="" >Siswa</option>
                <option value="" >Staf</option>
                <option value="" >Umum</option>
              </select>
            </div>
            <div class="row">
              <div class="col mb-3">
                <select class="form-control form-control-lg rounded-4" id="Tingkat" required>
                  <option value="" disabled>Tingkat</option>
                  <option value="10">10</option>
                  <option value="11">11</option>
                  <option value="12">12</option>
                </select>
              </div>
              <div class="col mb-3">
                <select class="form-control form-control-lg rounded-4" id="Jurusan" required>
                  <option value="" disabled>Jurusan</option>
                  <option value="pplg" >PPLG</option>
                  <option value="tbsm" >TBSM</option>
                  <option value="tjkt" >TJKT</option>
                  <option value="toi" >TOI</option>
                  <option value="dkv" >DKV</option>
                </select>
              </div>
              <div class="col mb-3">
                <select class="form-control form-control-lg rounded-4" id="Kelas" required>
                  <option value="" disabled>Kelas</option>
                  <option value="1">1</option>
                  <option value="2">2</option>
                  <option value="3">3</option>
                  <option value="4">4</option>
                </select>
              </div>
            </div>
            <div class="row mb-3">
              <select class="form-control form-control-lg rounded-4" id="Keperluan" required>
                <option value="" disabled>Keperluan</option>
                <option value="berkunjung">Berkunjung</option>
                <option value="membaca">Membaca Buku</option>
                <option value="mengembalikan">Mengembalikam Buku</option>
                <option value="meminjam">Meminjam Buku</option>
              </select>
            </div>
            <div class="row">
              <input class="form-control form-control-sm rounded-5" type="button" value="Submit">
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
  height: 100vh;
  width: 100%;
}
.p {
  background-image: linear-gradient(180deg, rgba(165, 160, 156, 0.3),rgba(72, 105, 133, 0.8), rgba(165, 160, 156, 0.3));
  border-radius: 50px;
  width: 15rem;
  margin: 15% 50% 5% 5%;
}

</style>