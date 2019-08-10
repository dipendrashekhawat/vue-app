<template>
  <div id="app">
    <img id="image" src="./assets/logo.png" alt="VueJS" />
    <h1>Employee Details</h1>
    <EmployeeDetails />
  </div>
</template>

<script>

import EmployeeDetails from './components/EmployeeDetails.vue'

export default {
  name: 'app',
  components: {
    EmployeeDetails
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 10px;
  margin-left: 10px;
}

#employee-details {
  width: 35%;
}

</style>
