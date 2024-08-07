<script setup>
import { RouterLink } from 'vue-router';
</script>
<template>
    <div class="container mt-30 d-flex column align-center">
        <div class="attention fs-50 mb-20"><i class="fa-solid fa-triangle-exclamation"></i></div>
        <h1 class="fs-not-mb-50 fs-mb-35 mb-20 fw-900">404 Not Found</h1>
        <div class="fs-25 fw-700 mb-30">This page does not exist</div>
        <RouterLink to="/">
            <button class="button-black py-15 r-15 fs-20">Go Back</button>
        </RouterLink>
    </div>
</template>
<style lang="scss" scoped>
@import '@/assets/styles/_variables';
.attention{
    color: #ffd43b;
}
button{
    background-color: $main-color;
}
</style>