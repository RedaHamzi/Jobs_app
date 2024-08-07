<script setup>
import Navbar from '@/components/Navbar.vue';
import '@/assets/myToolKit.css'
import { RouterView } from 'vue-router';

</script>

<template>
  <Navbar />
  <RouterView />
</template>

<style lang="scss">
@import '@/assets/styles/_variables';
</style>
