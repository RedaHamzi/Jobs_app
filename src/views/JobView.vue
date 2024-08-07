<script setup>
import BackButton from '@/components/BackButton.vue';
import { onMounted ,  ref } from 'vue';
import { RouterLink , useRoute , useRouter } from 'vue-router';
import { useToast } from 'vue-toastification';
import PulseLoader from 'vue-spinner/src/PulseLoader.vue';
import axios from 'axios';
const router = useRouter();
const toast = useToast();
const stat = ref({
    job : {},
    isLoading : true,
});
let route = useRoute();
let i = route.params.id;
onMounted(async () => {
    try{
        const response = await axios.get(`/api/jobs/${i}`);
        stat.value.job = response.data;
    }catch(err){
        console.error('The Error Is : ',err);
    }finally{
        stat.value.isLoading = false;
    };
});

const deleteJob = async () => {
    try{
        const confirm = window.confirm('Are You Sure ?!');
        if (confirm){
            await axios.delete(`/api/jobs/${i}`);
            router.push('/jobs');
            toast.success('The Job Deleted Succefuly');
        }
    }catch(err){
        console.error('Fetch Error',err);
        toast.success('The Job Not Deleted !');
    }
}

</script>
<template>
    <BackButton />
    <div v-if="stat.isLoading" class="t-center mt-20"><PulseLoader /></div>
    <section v-else class="job-view py-40 bg-light-green">
        <div class="container">
            <div class="grid gap-10 justify-center">
                <div class="lg-col-8 md-col-6 col-12 d-flex column gap-10">
                    <div class="box-shadow-card bg-white d-flex column gap-20 py-20 px-15 r-15">
                        <div class="c-grey">{{ stat.job.type }}</div>
                        <div class="fs-not-mb-40 fs-mb-35 fw-900">{{ stat.job.title }}</div>
                        <div class="c-red">{{ stat.job.location }}</div>
                    </div>
                    <!-- separator -->
                    <div class="box-shadow-card bg-white d-flex column gap-30 py-20 px-15 r-15">
                        <div class="d-flex column gap-20">
                            <div class="c-main-color fw-800 fs-20">Job Description</div>
                            <div class="fw-600 fs-18">{{ stat.job.description }}</div>
                        </div>
                        <div class="d-flex column gap-20">
                            <div class="c-main-color fw-800 fs-20">Salary</div>
                            <div class="fw-600 fs-18">{{ stat.job.salary }}</div>
                        </div>
                    </div>
                </div>
                <div class="lg-col-4 md-col-6 col-12 mb-col-12 d-flex column gap-10">
                    <div class="box-shadow-card bg-white d-flex column py-20 px-15 r-15">
                        <div class="fs-25 fw-800 mb-30">Company Info</div>
                        <div class="fs-not-mb-35 fs-mb-30 fw-600 mb-20">{{ stat.job.company.name }}</div>
                        <div class="company-description fs-17 fw-500 pb-20">
                            <p>{{ stat.job.company.description }}</p>    
                        </div>
                        <div class="contact d-flex column gap-20 pt-20">
                            <div class="d-flex column gap-10">
                                <div class="fs-not-mb-30 fs-mb-25 fw-600">Contact Email : </div>
                                <div class="p-10 bg-light-green fs-18 fw-800 r-5">{{ stat.job.company.contactEmail }}</div>
                            </div>
                            <!-- separator -->
                            <div class="d-flex column gap-10">
                                <div class="fs-not-mb-30 fs-mb-25 fw-600">Contact Phone : </div>
                                <div class="p-10 bg-light-green fs-18 fw-800 r-5">{{ stat.job.company.contactPhone }}</div>
                            </div>
                        </div>
                    </div>
                    <div class="box-shadow-card bg-white d-flex column py-20 px-15 r-15">
                        <div class="fs-25 fw-800 mb-30">Manage Job</div>
                        <RouterLink :to="`/jobs/edit/${stat.job.id}`">
                            <button class="button-black bg-green r-20 w-full fw-800 fs-20 py-10 mb-10">Edit Job</button>
                        </RouterLink>
                        <button @click="deleteJob" class="button-red r-20 w-full fw-800 fs-20 py-10 mb-10">Delete Job</button>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>
<style lang="scss" scoped>
@import '@/assets/styles/_variables.scss';
.bg{
    &-light-green{
        background-color: $light-green;
    }
    &-green{
        background-color: $green;
    }
}
.c{
    &-main-color{
        color : $main-color;
    }
    &-grey{
        color: #808080;
    }
    &-red{
        color: #FD0928;
    }
}
.box-shadow{
    &-card{
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2), 0 6px 20px rgba(0, 0, 0, 0.19);
    }
}
.job-view{
    .container{
        .company-description{
            line-height: 1.7;
            border-bottom: 1px solid $light-green;
        }
    }
}
</style>