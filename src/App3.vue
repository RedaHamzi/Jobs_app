<!-- <script>
import { ref } from 'vue';
export default{
  setup(){
    let name = ref('Hamzi Mohamed Reda');
    let states = ref('active');
    let tasks = ref(['taskOne' , 'taskTwo' , 'taskThree']);
    const toggleStates = () => {
      if (states.value == 'active'){
        states.value = 'pending'
      }else if(states.value == 'pending'){
        states.value = 'inactive'
      }else {
        states.value = 'active'
      }
    };
    return {
      name,
      states,
      tasks,
      toggleStates,
    }
  }
}

</script> -->
<script setup>
import { ref , onMounted } from 'vue';
let name = ref('Hamzi Mohamed Reda');
let states = ref('active');
let newTask = ref('');
let tasks = ref();
const toggleStates = () => {
  if (states.value == 'active'){
    states.value = 'pending'
  }else if(states.value == 'pending'){
    states.value = 'inactive'
  }else {
    states.value = 'active'
  }
};
const addSkill = () => {
  if (newTask.value.trim() !== ''){
    if ( !(tasks.value.includes(newTask.value)) ){
      tasks.value.push(newTask.value);
    }
  }
};
const deleteItem = (i) => {
  tasks.value.splice(i,1);
};
onMounted(async () => {
  try {
    let response = await fetch('https://jsonplaceholder.typicode.com/todos');
    let data = await response.json();
    tasks.value = data.map((task) => task.title)
  } catch(err){
    console.log('There Is An Error in fetching Data',err);
  }
})
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="states == 'active'">user Is {{ states }}</p>
  <p v-else-if="states == 'pending'">user Is Pendig</p>
  <p v-else>user Is Inactive</p>
  <form @click.prevent="addSkill">
    <label for="skill-name">Add a skill : </label>
    <input type="skill-name" id="skill-name" v-model="newTask">
    <button type="submit">Add</button>
  </form>
  <h3>Tasks :</h3>
  <ul>
    <li v-for="(task,index) in tasks" :key="task">
      <button @click="deleteItem(index)">x</button>
      <span>{{ task }}</span>
    </li>
  </ul>
  <hr>
  <button @click="toggleStates">Toggle</button>
</template>


<style scoped>
h1{
  color: red;
}
</style>