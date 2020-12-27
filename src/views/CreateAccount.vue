<template lang="pug">
  .container.is-fluid
    .form
      b-field(
        label="FirstName"
        :type="{'is-danger': formErrors.firstName}"
        :message="formErrors.firstName"
        )
        b-input(
          type="text"
          v-model="form.firstName"
          )
</template>

<script>
export default {
  data() {
    return {
      form: {
        firstName: "",
        lastName: "",
        username: "",
        password: "",
        confirmPassword: "",
      },
      formErrors: {
        firstName: "",
        lastName: "",
        username: "",
        password: "",
        confirmPassword: "",
      },
    };
  },
};
</script>

<style></style>
