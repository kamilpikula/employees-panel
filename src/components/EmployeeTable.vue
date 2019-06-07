<template>
  <div id="employee-table">
    <p v-if="employees.length < 1">
      No employees
    </p>
    <table v-else class="uk-table uk-table-striped uk-table-hover uk-table-divider">
      <thead>
        <tr>
          <th>Name</th>
          <th>Email</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="employee in employees" :key="employee.id">
          <td v-if="editing === employee.id">
            <input type="text"
                   v-model="employee.name"
                   class="uk-input" />
          </td>
          <td v-else>{{ employee.name }}</td>
          <td v-if="editing === employee.id">
            <input type="email"
                   v-model="employee.email"
                   class="uk-input" />
          </td>
          <td v-else>{{ employee.email }}</td>
          <td v-if="editing === employee.id">
            <button @click="editEmployee(employee)"
                    class="uk-button uk-button-default">Save</button>
            <button @click="editing = null"
                    class="uk-button uk-button-danger">Cancel</button>
          </td>
          <td v-else>
            <button @click="editMode(employee.id)"
                    class="uk-button uk-button-default">Edit</button>
            <button @click="$emit('delete:employee', employee.id)"
                    class="uk-button uk-button-danger">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'employee-table',
  props: {
    employees: Array,
  },
  data() {
    return {
      editing: null,
    }
  },
  methods: {
    editMode(id) {
      this.editing = id
    },

    editEmployee(employee) {
      if (employee.name === '' || employee.email === '') return
      this.$emit('edit:employee', employee.id, employee)
      this.editing = null
    }
  }
}
</script>

<style scoped>
.uk-button {
  margin-right: 10px;
}
</style>
