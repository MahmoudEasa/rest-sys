<template>
  <form @submit.prevent="onSubmit">
    <div class="row g-3 align-items-center">
      <h1>Sign Up</h1>

      <!-- User Name -->
      <div class="col-auto d-block mx-auto">
        <input
          v-model.trim="formData.username"
          type="text"
          class="form-control"
          placeholder="Enter Your Name"
        />
        <span class="text-danger" v-if="v$.formData.username.$error">
          {{ v$.formData.username.$errors[0].$message }}
        </span>
      </div>
    </div>
    <br />

    <!-- Email -->
    <div class="row g-3 align-items-center">
      <div class="col-auto d-block mx-auto">
        <input
          v-model.trim="formData.email"
          type="email"
          class="form-control"
          placeholder="Enter Your Email"
        />
        <span class="text-danger" v-if="v$.formData.email.$error">
          {{ v$.formData.email.$errors[0].$message }}
        </span>
      </div>
    </div>
    <br />

    <!-- Password -->
    <div class="row g-3 align-items-center">
      <div class="col-auto d-block mx-auto">
        <input
          v-model.trim="formData.password"
          type="password"
          class="form-control"
          placeholder="Enter Your password"
        />
        <span class="text-danger" v-if="v$.formData.password.$error">
          {{ v$.formData.password.$errors[0].$message }}
        </span>
      </div>
    </div>
    <br />

    <!-- Phone Number -->
    <div class="row g-3 align-items-center">
      <div class="col-auto d-block mx-auto">
        <input
          v-model.trim="formData.phone"
          type="text"
          class="form-control"
          placeholder="Enter Your Phone Number"
        />
        <span class="text-danger" v-if="v$.formData.phone.$error">
          {{ v$.formData.phone.$errors[0].$message }}
        </span>
      </div>
    </div>
    <br />

    <div class="row g-3 align-items-center">
      <div class="col-auto d-block mx-auto">
        <button type="submit" class="btn btn-primary">Sign Up Now</button>
        <button
          type="button"
          @click="redirectTo('LoginPage')"
          class="btn btn-link"
        >
          Login
        </button>
      </div>
    </div>
  </form>
</template>

<script>
import { mapActions } from "vuex";
import useValidate from "@vuelidate/core";
import { required, minLength, email, numeric } from "@vuelidate/validators";

export default {
  name: "SignUpForm",
  data() {
    return {
      v$: useValidate(),
      formData: {
        username: "",
        email: "",
        password: "",
        phone: "",
      },
    };
  },
  validations() {
    return {
      formData: {
        username: { required },
        email: { required, email },
        password: { required, minLength: minLength(6) },
        phone: { required, numeric },
      },
    };
  },
  methods: {
    ...mapActions(["redirectTo"]),

    onSubmit: function () {
      this.v$
        .$validate()
        .then((data) => {
          if (data) console.log(this.formData);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style></style>
