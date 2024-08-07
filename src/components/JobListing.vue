<script setup>
import { defineProps , ref } from 'vue';
import { RouterLink } from 'vue-router';
const props = defineProps({
    job : {
        type : Object,
    }
});
let isHidden = ref(true);
</script>

<template>
    <div class="col-12 lg-col-4 md-col-6">
        <div class="card d-flex column py-15 px-10 bg-white r-10">
            <div class="d-flex column pb-10">
                <div class="fs-15 mb-10">{{ job.type }}</div>
                <div class="fs-18 mb-20 fw-700">{{ job.title }}</div>
                <div :class="`fs-15 overflow-hidden ${ isHidden ? 'parent-height' : '' }`">
                    <p>{{ job.description }}</p>
                </div>
                <div class="more mb-17" @click="isHidden = !isHidden">{{ isHidden ? 'More' : 'Less' }}</div>
                <div class="salary">{{ job.salary }}</div>    
            </div>
            <div class="d-flex justify-space-between pt-10 align-center">
                <div><i class="fa-solid fa-location-dot"></i> {{ job.location }}</div>
                <RouterLink :to="`/jobs/${job.id}`">
                    <button class="button-black">Read More</button>
                </RouterLink>
            </div>
        </div>
    </div>
</template>
<style lang="scss" scoped>
@import '@/assets/styles/_variables.scss';
.parent-height{
    height: 60px;
}

.card{
    >div:first-child{
        border-bottom: 1px solid $light-green;
        div:nth-of-type(4),
        .salary{
            color: $green;
        }
        div:nth-of-type(4){
            cursor: pointer;
        }
    }
    >div:last-child{
        div{
            color: red;
        }
        button{
            background-color: $green;
        }
    }
}
</style>