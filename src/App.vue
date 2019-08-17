<template>
  <div id="app" class="small-container">
    <img id="image" src="./assets/logo.png" alt="VueJS" />
    <h1>Employee Details</h1>
    <employee-form  @add:employee="addEmployee" />

    <employee-details v-bind:employees ="employees"
                      @edit:employee="editEmployee"
                      @delete:employee="deleteEmployee"
    />
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
    async addEmployee(employee) {
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/users', {
          method: 'POST',
          body: JSON.stringify(employee),
          headers: { "Content-type": "application/json; charset=UTF-8" }
        })
        const data = await response.json()
        this.employees = [...this.employees, data]
      } catch (error) {
        console.error('Error occured while adding employee: ' +error)
      }
    },

    async getEmployees() {
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/users')
        const data = await response.json()
        this.employees = data
      } catch (error) {
        console.error('Error occured while retrieving employees: ' +error);
      }
    },

    async editEmployees(id, updatedEmployee) {
      try {
        const response = await fetch ('https://jsonplaceholder.typicode.com/users/${id}', {
          method: 'PUT',
          body: JSON.stringify(updatedEmployee),
          headers: { "Content-type": "application/json; charset=UTF-8" } 
        })

        const data = await response.json()
        this.employees = this.employees.map(employee => (employee.id === id ? data : employee))

      } catch (error) {
        console.error('Error while editing: ', +error)
      }
    }
  },
  mounted() {
    this.getEmployees()
  }
  
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
