<template lang="pug">
  .container.is-fluid
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
        label="Username"
        :type="{'is-danger': hasError('username')}"
        :message="getError('username')"
        )
        b-input(
          type="text"
          v-model="form.username"
          )
      b-field(
        label="Password"
        :type="{'is-danger': hasError('password')}"
        :message="getError('password')"
        )
        b-input(
          type="password"
          v-model="form.password"
          password-reveal
          )
      b-field(
        label="Confirm assword"
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
  name: "CreateAccount",
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
  methods: {
    checkLetterAndSpaces(text) {
      return /^[a-zA-Z ]+$/.test(text);
    },
    ensuresValidFirstName() {
      if (!this.checkLetterAndSpaces(this.form.firstName)) {
        return this.setError(
          "firstName",
          "Please write only letters and spaces."
        );
      }
      return this.setError("firstName", "");
    },
    ensuresValidLastName() {
      if (!this.checkLetterAndSpaces(this.form.lastName)) {
        return this.setError(
          "lastName",
          "Please write only letters and spaces."
        );
      }
      return this.setError("lastName", "");
    },
    ensuresValidUsername() {
      if (!/^[a-zA-Z_]+$/.test(this.form.username)) {
        return this.setError(
          "username",
          "Please write only letters and underscores."
        );
      }
      return this.setError("username", "");
    },
    ensuresValidPassword() {
      let validPassword;
      let validConfirmPassword;

      if (this.form.password <= 8 || !isNaN(Number(this.form.password))) {
        validPassword = this.setError(
          "password",
          "Please write more than 8 chars and not only numbers."
        );
      } else {
        validPassword = this.setError("password", "");
      }

      if (this.form.password !== this.form.confirmPassword) {
        validConfirmPassword = this.setError(
          "confirmPassword",
          "Both passwords must be the same."
        );
      } else {
        validConfirmPassword = this.setError("confirmPassword", "");
      }

      return validPassword && validConfirmPassword;
    },
    /**
     * @returns true if it's valid (errorMessage === ""), false if it's invalid.
     */
    setError(key, errorMessage) {
      this.formErrors[key] = errorMessage;
      return errorMessage === "";
    },
    hasError(key) {
      return (
        Object.prototype.hasOwnProperty.call(this.formErrors, key) &&
        this.formErrors[key] !== ""
      );
    },
    getError(key) {
      return this.hasError(key) ? this.formErrors[key] : "";
    },
    handleSubmit() {
      const validFirstName = this.ensuresValidFirstName();
      const validLastName = this.ensuresValidLastName();
      const validUsername = this.ensuresValidUsername();
      const validPassword = this.ensuresValidPassword();

      if (validFirstName && validLastName && validUsername && validPassword) {
        alert("User created!");
      }
    },
  },
};
</script>

<style></style>
