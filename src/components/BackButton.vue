<script setup>
import { RouterLink } from 'vue-router';
</script>
<template>
    <section class="py-30 bg-white">
        <div class="container">
            <RouterLink to="/jobs" class="d-flex align-center gap-10">
                <div class="c-green"><i class="fa-solid fa-arrow-left"></i></div>
                <div class="c-green fw-600 fs-18">Back to Job Listings</div>
            </RouterLink>
        </div>
    </section>
</template>
<style lang="scss" scoped>
@import '@/assets/styles/_variables';
.c-green{
    color: $green;
}
</style>