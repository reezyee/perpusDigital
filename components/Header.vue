<template>
  <div class="row navbar navbar-expand-lg bg-transparant m-0 position-fixed">
    <div class="col-2" style="padding-left: 8%;">
      <img src="@/assets/img/LOGO-SMK4.png" alt="logo smkn4">
    </div>
    <div class="col" style="color: white;">
      <p class="judul ms-4">Perpus Digital</p>
      <p class="alamat ms-4">SMK Negeri 4 Tasikmalaya</p>
    </div>
  </div>
</template>

<script setup>

</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Chau+Philomene+One&family=Jockey+One&family=Jomhuria&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Jaldi:wght@400;700&display=swap');

.bg-transparant{
  background-color: #45618860; 
  width: 100%;
  box-shadow: 1px 1px 6px 0px;
}

.judul {
  letter-spacing: 10px;
  font-family: "Jockey One";
  font-size: 60px;
}

.alamat {
  font-family: "Jaldi"; 
  font-size: 20px;
}

img {
  width: 115px;
}

@media (max-width: 912px){
  img {
    width: 90px;
  }
}
@media (max-width: 600px){
  img {
    width: 70px;
  }
  .judul {
  letter-spacing: 10px;
  font-size: 30px;
  font-family: "Jockey One";
  padding-left: 20px;
  }
  .alamat {
  font-family: "Jaldi";  
  padding-left: 20px; 
  }
}
</style>