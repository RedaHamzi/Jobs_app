<script setup>
import { ref , defineProps , onMounted } from 'vue';
import JobListing from '@/components/JobListing.vue';
import PulseLoader from 'vue-spinner/src/PulseLoader.vue';
const myJobs = ref({
    jobs : [],
    isLoading : true
});
const props = defineProps({
    limit : {
        type : Number,
    },
    display : Boolean,
})
let isClicked = ref(false);
onMounted(async () => {
    try{
        const response = await fetch('/api/jobs');
        const data = await response.json();
        myJobs.value.jobs = data;
    }catch(err){
        console.error(`This Is An Error : ${err}`);
    } finally{
        myJobs.value.isLoading = false;
    }
})
</script>
<template>
    <section class="jobs">
        <div class="container d-flex column gap-25">
            <h1 class="fs-not-mb-35 fs-mb-25 t-center">
                Browse Jobs
            </h1>
            <div v-if="myJobs.isLoading" class="c-black t-center fs-30"><PulseLoader /></div>
            <div v-else-if="!isClicked" class="grid gap-10">
                <jobListing  v-for="myJob in myJobs.jobs.slice(0,limit || myJobs.length)" :key="myJob" :job="myJob" />
            </div>
            <div v-else class="grid justify-center gap-10">
                <jobListing  v-for="myJob in myJobs.jobs" :key="myJob" :job="myJob" />
            </div>
        </div>
    </section>
    <section v-if="display" class="py-30 flex-center bg-white">
        <button @click="isClicked = !isClicked" class="button-black fs-18 py-15">{{ isClicked ? 'Less Jobs' : 'View All Jobs' }}</button>
    </section>
</template>
<style lang="scss" scoped>
@import '@/assets/styles/_variables.scss';
.jobs{
    padding : 50px 0;
    background-color: $light-green;
    @include break-point(mobile){
        padding : 30px 0;
    }
    .container{
        h1{
            color: $green;
        }
    }
}
button{
    width: 300px;
}
</style>