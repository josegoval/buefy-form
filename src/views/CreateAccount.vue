<template lang="pug">
  .container.is-fluid
    CreateUserForm(:form="form" :formErrors="formErrors" :handleSubmit="handleSubmit")
</template>

<script>
import CreateUserForm from "@/components/CreateUserForm.vue";

export default {
  name: "CreateAccount",
  components: {
    CreateUserForm,
  },
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
    isValidFirstName() {
      this.setError("firstName", "");

      if (
        this.form.firstName !== "" &&
        !this.checkLetterAndSpaces(this.form.firstName)
      ) {
        this.setError("firstName", "Please write only letters and spaces.");
      }

      return !this.hasError("firstName");
    },
    isValidLastName() {
      this.setError("lastName", "");

      if (
        this.form.lastName !== "" &&
        !this.checkLetterAndSpaces(this.form.lastName)
      ) {
        this.setError("lastName", "Please write only letters and spaces.");
      }

      return !this.hasError("lastName");
    },
    isValidUsername() {
      this.setError("username", "");

      if (!/^[a-zA-Z_]+$/.test(this.form.username)) {
        this.setError("username", "Please write only letters and underscores.");
      }

      return !this.hasError("username");
    },
    isValidPassword() {
      this.setError("password", "");
      this.setError("confirmPassword", "");

      if (
        this.form.password.length <= 8 ||
        !isNaN(Number(this.form.password))
      ) {
        this.setError(
          "password",
          "Please write more than 8 chars and not only numbers."
        );
        return false;
      }

      if (this.form.password !== this.form.confirmPassword) {
        this.setError("confirmPassword", "Both passwords must be the same.");
        return false;
      }

      return true;
    },
    isValidForm() {
      const validFirstName = this.isValidFirstName();
      const validLastName = this.isValidLastName();
      const validUsername = this.isValidUsername();
      const validPassword = this.isValidPassword();

      return validFirstName && validLastName && validUsername && validPassword;
    },
    hasError(key) {
      return (
        Object.prototype.hasOwnProperty.call(this.formErrors, key) &&
        this.formErrors[key] !== ""
      );
    },
    setError(key, errorMessage) {
      this.formErrors[key] = errorMessage;
    },
    handleSubmit() {
      if (!this.isValidForm()) {
        return;
      }

      alert("User created!");
    },
  },
};
</script>

<style></style>
