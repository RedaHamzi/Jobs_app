<script setup>
import { onMounted, ref } from 'vue';
import { useRouter } from 'vue-router';
import { useToast } from 'vue-toastification';
import axios from 'axios';
const toast = useToast();
const router = useRouter();
let salaries = ref(['under$50K','$50K-$60K','$60K-$70K','$70K-$80K','$90K-$100K','$100K-$110K','$100K-$125K','$125K-$150K','$150K-$175K','$175K-$200K','Over$200K']);
const form = ref({
    title: "",
    type: "",
    description: "",
    location: "",
    salary: "",
    company: {
        name: "",
        description: "",
        contactEmail: "",
        contactPhone: "",
    }
});
const addNew = async (event) => {
    event.preventDefault(); // Prevent the default form submission behavior
    const newJob = {
        title: form.value.title,
        type: form.value.type,
        description: form.value.description,
        location: form.value.location,
        salary: form.value.salary,
        company: {
            name: form.value.company.name,
            description: form.value.company.description,
            contactEmail: form.value.company.contactEmail,
            contactPhone: form.value.company.contactPhone,
        }
    };
    try{
        const response = await axios.post('/api/jobs',newJob);
        router.push(`/jobs/${response.data.id}`);
        toast.success('The Job Was Added Succefuly');
    }catch(err){
        console.error('Post Error',err);
        toast.error('The Job Was not Added');
    }
};
</script>
<template>
    <section class="add-job bg-light-green">
        <div class="container">
            <form @submit="addNew" class="bg-white r-10 py-30 px-20">
                <div class="fs-40 t-center fw-900 mb-30">Add Job</div>
                <div class="d-flex column gap-20 fs-20">
                    <div class="d-flex column gap-15">
                        <label for="job-type" class="fw-700">Job Type : </label>
                        <div>
                            <select required id="job-type" v-model="form.type" class="w-full border r-10 py-15 px-10 fs-18 border">
                                <option value="Full-Time">Full-Time</option>
                                <option value="Part_time">Part_time</option>
                            </select>
                        </div>  
                    </div>
                    <!-- separator -->
                    <div class="d-flex column gap-15">
                        <label for="job-listing" class="fw-700">Job Listing Name : </label>
                        <input required v-model="form.title" type="text" id="job-listing" placeholder="eg. Beautiful Apartment in Miami" 
                        class="fs-18 w-full border r-10 py-15 px-10">  
                    </div>
                    <!-- separator -->
                    <div class="d-flex column gap-15">
                        <label for="description" class="fw-700">Description : </label>
                        <textarea required v-model="form.description" id="description" class="w-full border r-10 py-15 px-10 fw-600 fs-18" name="description" rows="6"
                        placeholder="Add any job duties, expectations, requirements, etc"></textarea>
                    </div>
                    <div class="d-flex column gap-15">
                        <label for="salary" class="fw-700">Salary : </label>
                        <select v-model="form.salary" required id="salary" class="w-full border r-10 py-15 px-10 fs-18 border">
                            <option v-for="salary in salaries" :key="salary" class="fw-500" :value="salary">{{salary}}</option>
                        </select>  
                    </div>
                    <!-- separator -->
                    <div class="d-flex column gap-15">
                        <label for="location" class="fw-700">Location : </label>
                        <input required v-model="form.location" type="text" id="location" placeholder="Company Location" 
                        class="fs-18 w-full border r-10 py-15 px-10">  
                    </div>
                    <!-- separator -->
                    <div class="fs-30 fw-600 my-15">Company Info</div>
                    <!-- separator -->
                    <div class="d-flex column gap-15">
                        <label for="company-name" class="fw-700">Company Name : </label>
                        <input required v-model="form.company.name" type="text" id="company-name" placeholder="Company Name" 
                        class="fs-18 w-full border r-10 py-15 px-10">  
                    </div>
                    <!-- separator -->
                    <div class="d-flex column gap-15">
                        <label for="company-description" class="fw-700">Company Description : </label>
                        <textarea required v-model="form.company.description" id="company-description" class="w-full border r-10 py-15 px-10 fw-600 fs-18" name="description" rows="6"
                        placeholder="Company Description"></textarea>
                    </div>
                    <!-- separator -->
                    <div class="d-flex column gap-15">
                        <label for="email" class="fw-700">Contact Email : </label>
                        <input required v-model="form.company.contactEmail" type="text" id="email" placeholder="Email Adress" 
                        class="fs-18 w-full border r-10 py-15 px-10">  
                    </div>
                    <!-- separator -->
                    <div class="d-flex column gap-15">
                        <label for="phone" class="fw-700">Contact Phone : </label>
                        <input required v-model="form.company.contactPhone" type="text" id="phone" placeholder="Optional phone for applicants" 
                        class="fs-18 w-full border r-10 py-15 px-10">  
                    </div>
                    <!-- separator -->
                    <input name="submit" type="submit" value="Add Job" class="button-black w-full r-25 bg-green fs-18 py-15">
                    <!-- <button type="submit" class="button-black w-full r-25 bg-green fs-18 py-15">Add job</button> -->
                </div>
            </form>
        </div>
    </section>
</template>
<style lang="scss" scoped>
@import '@/assets/styles/_variables';
textarea{
    font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}
.bg-light-green{
    background-color: $light-green;
}
.bg-green{
    background-color: $green;
}
.border{
    border: 2px solid #ccc;
    &:focus{
        border: 2px solid #868585;
    }
}
*::placeholder{
    font-weight: 500;
    font-size: 17px;
}
.add-job{
    padding: 60px 0;
    @include break-point(mobile){
        padding: 40px;
    }
    .container{
        form{
            border: 1px solid $green;
            select {
                outline: none;
                cursor: pointer;
            }
            option{
                line-height: 2;
                background-color: black;
                color: white;
                &:hover{
                    background-color: white;
                    color: black;
                }
            }
        }
    }
}

</style>