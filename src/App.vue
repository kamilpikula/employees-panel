<template>
  <div id="app">
    <h1 class="uk-heading-small">Employees</h1>
    <employee-table :employees="employees" @delete:employee="deleteEmployee" />
  </div>
</template>

<script>
import EmployeeTable from '@/components/EmployeeTable.vue'

export default {
  name: 'app',
  components: {
    EmployeeTable,
  },
  data() {
    return {
      employees: [
        {
          name: 'Jakub Nowak',
          email: 'jnowak@poczta.onet.pl',
        },
        {
          name: 'Dorota Kowalska',
          email: 'dkowalska19@gmail.com',
        },
        {
          name: 'Krzysztof Ignaczak',
          email: 'ignaczak.krzysztof@gmail.com',
        },
      ],
    }
  },
  methods: {
    deleteEmployee(id) {
    this.employees = this.employees.filter(
      employee => employee.id !== id
    )
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
