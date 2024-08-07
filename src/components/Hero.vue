<template>
<section class="landing py-30 flex-center">
<div class="container d-flex column align-center gap-20 c-white">
  <h1 class="fw-900 fs-mb-30 fs-not-mb-40">Become a Vue dev</h1>
  <p class="fs-20 t-center">Find the Vue job that fits your skills and needs</p>
</div>
</section>
</template>

<style lang="scss">
@import '@/assets/styles/_variables';
.landing{
  background-color: $main-color;
  @include break-point(mobile){
    height: 50vh;
  }
}

</style>





