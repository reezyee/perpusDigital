<template>
  <div class="row navbar navbar-expand-lg bg-transparant m-0 position-fixed z-1">
    <div class="col-md-2 col-3" style="padding-left: 8%;">
      <img class="img-fluid" src="@/assets/img/LOGO-SMK4.png" alt="logo smkn4">
    </div>
    <div class="col-md-10 col-9" style="color: white;">
      <h1 class="judul ">Perpus Digital</h1>
      <p class="alamat">SMK Negeri 4 Tasikmalaya</p>
    </div>
  </div>
</template>

<script setup>

</script>

<style scoped>

.bg-transparant{
  background-color: #45618860; 
  width: 100%;
  box-shadow: 1px 1px 6px 0px;
}

.judul {
  letter-spacing: 10px;
  font-family: "Jockey One";
  font-size: 50px;
}

.alamat {
  font-family: "Jaldi"; 
  font-size: 20px;
}

img {
  width: 100px;
}
/* 
@media (max-width: 912px){
  img {
    width: 90px;
  }
  .judul {
    letter-spacing: 10px;
    font-size: 50px;
    font-family: "Jockey One";
    padding-left: 20px;
  }
  .alamat {
    font-family: "Jaldi";  
    padding-left: 20px; 
  }
}
@media (max-width: 600px){
  img {
    width: 70px;
  }
  .alamat {
    font-family: "Jaldi";  
    padding-left: 20px; 
  }
} */
</style>