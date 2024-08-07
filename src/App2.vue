<script>
export default{
  data(){
    return {
      name : 'Reda',
      states : 'reda',
      tasks : ['Bla' ,'Something','Also'],
      mySite : 'https://redahamzi.github.io/RYL-WebFrontEnd/index.html',
    }
  },
  methods : {
    toggleStates(){
      if (this.states == 'active'){
        this.states = 'pending'
      }else if(this.states == 'pending'){
        this.states = 'inactive'
      }else {
        this.states = 'active'
      }
    }
  }
}

</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="states == 'active'">user Is {{ states }}</p>
  <p v-else-if="states == 'pending'">user Is Pendig</p>
  <p v-else>user Is Inactive</p>
  <h3>Tasks :</h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>
  <br>
  <hr>
  <button @click="toggleStates">Toggle</button>
</template>


<style scoped>
h1{
  color: red;
}
</style>