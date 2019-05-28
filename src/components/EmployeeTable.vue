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
          <td>{{ employee.name }}</td>
          <td>{{ employee.email }}</td>
          <td>
            <button class="uk-button uk-button-default">Edit</button>
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
  }
}
</script>

<style scoped>
.uk-button {
  margin-right: 10px;
}
</style>
