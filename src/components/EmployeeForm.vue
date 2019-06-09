<template>
<div class="uk-card uk-card-default uk-card-body">
  <h1 class="uk-heading-small">Employees</h1>
<form @submit.prevent="handleSubmit">
  <div class="uk-margin">
    <div class="uk-inline">
      <span class="uk-form-icon" uk-icon="icon: user"></span>
      <input ref="first"
             type="text"
             :class="{ 'uk-form-danger': submitting && invalidName }"
             v-model="employee.name"
             @focus="clearStatus"
             @keypress="clearStatus"
             class="uk-input"
             placeholder="Employee name">
    </div>
  </div>
  <div class="uk-margin">
    <div class="uk-inline">
      <span class="uk-form-icon" uk-icon="icon: mail"></span>
      <input type="email"
             :class="{ 'uk-form-danger': submitting && invalidEmail }"
             v-model="employee.email"
             @focus="clearStatus"
             class="uk-input"
             placeholder="Email">
    </div>
  </div>
  <div v-if="error && submitting" class="uk-alert-danger" uk-alert>
    <a class="uk-alert-close" uk-close></a>
    Please fill out all required fields!
  </div>
  <div v-if="success" class="uk-alert-success" uk-alert>
    <a class="uk-alert-close" uk-close></a>
    Employee successfully added
  </div>
  <button class="uk-button uk-button-primary" uk-icon="icon: triangle-right">Add Employee</button>
</form>
</div>
</template>

<script>
export default {
  name: 'employee-form',
  data() {
    return {
      submitting: false,
      error: false,
      success: false,
      employee: {
        name: '',
        email: '',
      },
    }
  },
  methods: {
    handleSubmit() {
      this.submitting = true
      this.clearStatus()

      if (this.invalidName || this.invalidEmail) {
        this.error = true
        return
      }

      this.$emit('add:employee', this.employee)
      this.$refs.first.focus()
      this.employee = {
        name: '',
        email: '',
      }
      this.error = false
      this.success = true
      this.submitting = false
    },

    clearStatus() {
      this.success = false
      this.error = false
    },
  },

  computed: {
    invalidName() {
      return this.employee.name === ''
    },
    invalidEmail() {
      return this.employee.email === ''
    },
  },
}
</script>

<style scoped>
  form {
    margin-bottom: 2rem;
  }

  [class*='-message'] {
    font-weight: 500;
  }
</style>
