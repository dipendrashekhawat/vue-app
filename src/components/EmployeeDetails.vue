<template>
  <div id="employee-details">
    <p v-if="employees.length < 1">
      No employees
    </p>
    <table v-else>
      <thead>
        <tr>
          <th>Name</th>
          <th>Email</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="employee in employees" v-bind:key="employee.id">
          <td v-if="editing === employee.id">
            <input
              type="text"
              v-model="employee.name"
            >
          </td>
          <td v-else>{{ employee.name }}</td>

          <td v-if="editing === employee.id">
            <input
              type="text"
              v-model="employee.email"
            >
          </td>
          <td>{{ employee.email }}</td>

          <td v-if="editing === employee.id">
            <button @click="editEmployee(employee)">Save</button>
            <button
              class="muted-button"
              @click="cancelEdit(employee)"
            >Cancel</button>
          </td>
          <td v-else>
            <button @click="editMode(employee)">Edit</button>
            <button @click="$emit('delete:employee', employee.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  export default {
    name: 'employee-details',
    props: {
      employees: Array,
    },

    data() {
      return {
        editing: null,
      }
    },

    methods: {
      editMode(employee) {
        this.cachedEmployee

      },
    }
  }
</script>

<style scoped></style>