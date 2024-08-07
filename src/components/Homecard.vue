<script setup>
import { RouterLink } from 'vue-router';
</script>
<template>
<section class="home-card">
    <div class="container grid gap-20">
        <div class="md-col-6 col-12">
            <div class="card bg-light-grey d-flex r-15 column gap-15 py-25 px-22">
                <h2 class="fw-700 fs-not-mb-25">For Developers</h2>
                <p class="fw-500 fs-not-mb-17">Browse our Vue jobs and start your creer today</p>
                <RouterLink to="/jobs">
                    <button class="button-black py-15 fs-17">Browse Jobs</button>
                </RouterLink>
            </div>
        </div>
        <!-- seperator -->
        <div class="md-col-6 col-12">
            <div class="card bg-light-green d-flex r-15 column gap-15 w-fit py-25 px-20">
                <h2 class="fw-700 fs-not-mb-25">For Employers</h2>
                <p class="fw-500 fs-not-mb-17">List your job to find the perfect developer for the role</p>
                <RouterLink to="/jobs/add">
                    <button class="button-black bg-green w-fit py-15 fs-17">Add Job</button>
                </RouterLink>
            </div>
        </div>

    </div>
</section>
</template>

<style lang="scss" scoped>
@import '@/assets/styles/_variables';
.bg{
    &-light-green{
        background-color: $light-green;
    }
    &-light-grey{
        background-color: $light-grey;
    }
    &-green{
        background-color: $green;

    }

}
.home-card{
    padding : 50px 0;
    @include break-point(mobile){
        padding : 30px 0;
    }
    .container{
        @include break-point(mobile){
            flex-direction: column;
        }
        .card{
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2), 0 6px 20px rgba(0, 0, 0, 0.19);
            transition: box-shadow 0.3s ease-in-out, transform 0.3s ease-in-out;
            &:hover{
                box-shadow: 0 16px 24px rgba(0, 0, 0, 0.4);
                transform: translateY(-10px);
            }
            p{
                line-height : 1.7;
            }
        }
    }
}
</style>
    
    
    
    
    
    