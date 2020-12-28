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
    ensuresValidFirstName() {
      if (
        this.form.firstName !== "" &&
        !this.checkLetterAndSpaces(this.form.firstName)
      ) {
        return !this.setError(
          "firstName",
          "Please write only letters and spaces."
        );
      }
      return !this.setError("firstName", "");
    },
    ensuresValidLastName() {
      if (
        this.form.lastName !== "" &&
        !this.checkLetterAndSpaces(this.form.lastName)
      ) {
        return !this.setError(
          "lastName",
          "Please write only letters and spaces."
        );
      }
      return !this.setError("lastName", "");
    },
    ensuresValidUsername() {
      if (!/^[a-zA-Z_]+$/.test(this.form.username)) {
        return !this.setError(
          "username",
          "Please write only letters and underscores."
        );
      }
      return !this.setError("username", "");
    },
    ensuresValidPassword() {
      const validPassword =
        this.form.password.length <= 8 || !isNaN(Number(this.form.password))
          ? !this.setError(
              "password",
              "Please write more than 8 chars and not only numbers."
            )
          : !this.setError("password", "");
      const validConfirmPassword =
        this.form.password !== this.form.confirmPassword
          ? !this.setError(
              "confirmPassword",
              "Both passwords must be the same."
            )
          : !this.setError("confirmPassword", "");

      return validPassword && validConfirmPassword;
    },
    /**
     * @returns true if it's has an error (errorMessage !== "")
     */
    setError(key, errorMessage) {
      this.formErrors[key] = errorMessage;
      return errorMessage !== "";
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
