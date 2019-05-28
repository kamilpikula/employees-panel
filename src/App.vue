<template>
  <div id="app">
    <h1 class="uk-heading-small">Employees</h1>
    <employee-form @add:employee="addEmployee" />
    <employee-table :employees="employees"/>
  </div>
</template>

<script>
import EmployeeForm from '@/components/EmployeeForm.vue'
import EmployeeTable from '@/components/EmployeeTable.vue'

export default {
  name: 'app',
  components: {
    EmployeeForm,
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
    addEmployee(employee) {
      const lastId = this.employees.length > 0 ? this.employees[this.employees.length - 1].id : 0;
      const id = lastId + 1;
      const newEmployee = { ...employee, id};

      this.employees = [...this.employees, newEmployee];
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
