<style lang="scss" scoped>
@import '@/assets/styles/_variables';
.active {
  background-color: rgba($color: #000000, $alpha: 0.5);
}
nav {
  border-bottom: 2px solid white;
  background-color: $main-color;
  .container {
    height: 100%;
    .vueLogo {
      img {
        width: 35px;
        height: auto;
        transform: translateY(5px);
      }
    }
    .links {
      a {
        transition: all 0.5s;
        &:hover {
          background-color: rgba($color: #000000, $alpha: 0.8);
        }
      }
    }
  }
}
</style>

<template>
  <nav id="navBar">
    <div class="container py-20 px-50 d-flex gap-10 align-center justify-space-between">
      <div class="vueLogo p-7 bg-white r-50 r-circle">
        <img :src="logo" alt="">
      </div>
      <div class="links fs-not-mb-20 fs-mb-15 d-flex align-center gap-20">
        <RouterLink to="/" :class="`d-block c-white p-10 r-5 ${activeLink('/') ? 'active' : '' }`">Home</RouterLink>
        <RouterLink to="/jobs" :class="`d-block c-white p-10 r-5 ${activeLink('/jobs') ? 'active' : '' }`">Jobs</RouterLink>
        <RouterLink to="/jobs/add" :class="`d-block c-white p-10 r-5 ${activeLink('/jobs/add') ? 'active' : '' }`">Add Job</RouterLink>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { RouterLink , useRoute } from 'vue-router';
import logo from '@/assets/logo.svg';
const activeLink = (routerPath) => {
  const route = useRoute();
  return route.path == routerPath;
};
</script>

