<script setup>
import Hero from '@/components/Hero.vue';
import JobListings from '@/components/JobListings.vue';
import Homecard from '@/components/Homecard.vue';
import { onMounted, ref , defineProps } from 'vue';
onMounted(() => {
  const navBar = document.getElementById('navBar');
  if (navBar) {
    const height = navBar.offsetHeight;
    const landing = document.querySelector('.landing');
    if (landing) {
      landing.style.height = `${100 - height / window.innerHeight * 100}vh`;
    }
  }
});
let limit = ref(3);
let display = true;
</script>

<template>
    <Hero />
    <Homecard />
    <JobListings :limit="limit" :display="display"/>
</template>