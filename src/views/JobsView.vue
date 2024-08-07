<script setup>
import Homecard from '@/components/Homecard.vue';
import JobListings from '@/components/JobListings.vue';
let display = false
</script>
<template>
    <Homecard />
    <JobListings :btnDisplay="display"/>
</template>