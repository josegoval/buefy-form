<template lang="pug">
    .form
      .title Create a new account
      b-field(
        label="First name"
        :type="{'is-danger': hasError('firstName')}"
        :message="getError('firstName')"
        )
        b-input(
          type="text"
          v-model="form.firstName"
          )
      b-field(
        label="Last name"
        :type="{'is-danger': hasError('lastName')}"
        :message="getError('lastName')"
        )
        b-input(
          type="text"
          v-model="form.lastName"
          )
      b-field(
        label="Username*"
        :type="{'is-danger': hasError('username')}"
        :message="getError('username')"
        )
        b-input(
          type="text"
          v-model="form.username"
          )
      b-field(
        label="Password*"
        :type="{'is-danger': hasError('password')}"
        :message="getError('password')"
        )
        b-input(
          type="password"
          v-model="form.password"
          password-reveal
          )
      b-field(
        label="Confirm password*"
        :type="{'is-danger': hasError('confirmPassword')}"
        :message="getError('confirmPassword')"
        )
        b-input(
          type="password"
          v-model="form.confirmPassword"
          password-reveal
          )
      b-button(
        type="is-primary"
        @click="handleSubmit"
      ) Submit
</template>

<script>
export default {
  name: "CreateUserForm",
  props: {
    form: {
      type: Object,
      required: true,
    },
    formErrors: {
      type: Object,
      required: true,
    },
    handleSubmit: {
      type: Function,
      required: true,
    },
  },
  methods: {
    hasError(key) {
      return (
        Object.prototype.hasOwnProperty.call(this.formErrors, key) &&
        this.formErrors[key] !== ""
      );
    },
    getError(key) {
      return this.hasError(key) ? this.formErrors[key] : "";
    },
  },
};
</script>

<style></style>
