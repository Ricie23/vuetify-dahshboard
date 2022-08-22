<template>
    <v-container>
        <v-row>
            <v-col>
                <v-form ref="signUpForm" v-model="formValidity">
                    <v-text-field label="Email" type="email" v-model="email" :rules="emailRules"/>
                    <v-autocomplete label="Which browser do you use?" :items="browsers"/>
                    <v-file-input label="Attach Profile Picture"/>
                    <v-text-field label="Birthday" v-model="birthday" readonly/>
                    <v-date-picker cols="6" v-model="birthday"/>
                    <v-checkbox label="Agree to Terms and Conditions" v-model="agreeToTerms" :rules="agreeToTermRules" required/>
                    <v-btn class="mr-4" :disabled="!formValidity" type="submit" color="primary">Submit</v-btn>
                    <v-btn class="mr-4" color="success" @click="validateForm">Validate Form</v-btn>
                    <v-btn class="mr-4" color="warning" @click="resetValidation">Reset Validation</v-btn>
                    <v-btn class="mr-4" color="error" @click="resetForm">Reset Form</v-btn>
                </v-form>
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
export default {
  data() {
    return {
      formValidity: false,
      birthday: "",
      agreeToTerms: false,
      email: "",
      browsers: ["Chrome", "Firefox", "Safari", "Edge", "Brave"],
      agreeToTermRules: [(value) => !!value || "You must agree to the terms"],
      emailRules: [
        (value) => !!value || "Email is required.",
        (value) => value.indexOf("@") !== 0 || "Email should have a username.",
        (value) => value.includes("@") || "Email should have @ symbol. ",
        (value) =>
          value.indexOf(".") - value.indexOf("@") > 1 ||
          "Email must contain a domain name.",
        (value) =>
          value.indexOf(".") <= value.length - 3 ||
          "email must have a proper domian extension",
      ],
    };
  },
  methods: {
    resetValidation() {
      this.$refs.signUpForm.resetValidation();
    },
    resetForm() {
      this.$refs.signUpForm.reset();
    },
    validateForm() {
      this.$refs.signUpForm.validate();
    },
  },
};
</script>

<style scoped>
</style>