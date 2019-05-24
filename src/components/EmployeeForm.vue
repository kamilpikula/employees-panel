<template>
<form>
  <div class="uk-margin">
    <div class="uk-inline">
      <span class="uk-form-icon" uk-icon="icon: user"></span>
      <input class="uk-input" type="text" placeholder="Employee name">
    </div>
  </div>
  <div class="uk-margin">
    <div class="uk-inline">
      <span class="uk-form-icon" uk-icon="icon: mail"></span>
      <input class="uk-input" type="text" placeholder="Email">
    </div>
  </div>
  <button class="uk-button uk-button-primary" uk-icon="icon: triangle-right">Add Employee</button>
</form>
</template>

<script>
export default {
  name: 'employee-form',
  data() {
    return {
      employee: {
        name: '',
        email: '',
      },
    }
  },
}
</script>

<style scoped>

</style>
