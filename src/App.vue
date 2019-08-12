<template>
  <div id="app" class="small-container">
    <img id="image" src="./assets/logo.png" alt="VueJS" />
    <h1>Employee Details</h1>
    <employee-form  @add:employee="addEmployee" />
    <employee-details v-bind:employees ="employees" />
  </div>
</template>

<script>

import EmployeeForm from './components/EmployeeForm.vue'
import EmployeeDetails from './components/EmployeeDetails.vue'


export default {
  name: 'app',
  components: {
    EmployeeDetails,
    EmployeeForm,
  },
  data() {
    return {
      employees: [],
    }
  },
  methods: {
    addEmployee(employee){
    const lastId = this.employees.length > 0 ? this.employees[this.employees.length - 1].id : 0;
    const id = lastId + 1;
    const newEmployee = { ...employee, id };
    
    this.employees = [...this.employees, newEmployee]
    }
  },
  
  }
</script>

<style>

#employee-details {
  width: 80%;
}

button {
  background: #009435;
  border: 1px solid #009435;
}

.small-container {
  max-width: 680px;
   font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 10px;
  margin-left: 10px;
}

</style>
