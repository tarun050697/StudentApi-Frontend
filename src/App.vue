<template>
  <StudentData/>
  
</template>

<script>
import StudentData from './components/StudentData'

import "@hennge/vue3-pagination/dist/vue3-pagination.css";



export default {
  name: 'App',
  components: {
    StudentData,
    
    
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
