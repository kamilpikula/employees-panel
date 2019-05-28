<template>
<form @submit.prevent="handleSubmit">
  <div class="uk-margin">
    <div class="uk-inline">
      <span class="uk-form-icon" uk-icon="icon: user"></span>
      <input ref="first"
             type="text"
             :class="{ 'has-error': submitting && invalidName }"
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
             :class="{ 'has-error': submitting && invalidEmail }"
             v-model="employee.email"
             @focus="clearStatus"
             class="uk-input"
             placeholder="Email">
    </div>
  </div>
  <p v-if="error && submitting" class="error-message">
    Please fill out all required fields!
  </p>
  <p v-if="success" class="success-message">
    Employee successfully added
  </p>
  <button class="uk-button uk-button-primary" uk-icon="icon: triangle-right">Add Employee</button>
</form>
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

  .has-error {
    border: 1px solid #d33c40;
  }

  .error-message {
    color: #d33c40;
  }

  .success-message {
    color: #32a95d;
  }
</style>
