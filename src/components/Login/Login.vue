<template>
  <form @submit.prevent="onSubmit">
    <div class="row g-3 align-items-center">
      <h1>Login</h1>

      <!-- Email -->
      <div class="col-auto d-block mx-auto">
        <input
          v-model.trim="state.email"
          type="email"
          class="form-control"
          placeholder="Enter Your Email"
        />
        <span class="text-danger" v-if="v$.email.$error">
          {{ v$.email.$errors[0].$message }}
        </span>
      </div>
    </div>
    <br />

    <!-- Password -->
    <div class="row g-3 align-items-center">
      <div class="col-auto d-block mx-auto">
        <input
          v-model.trim="state.password"
          type="password"
          class="form-control"
          placeholder="Enter Your password"
        />
        <span class="text-danger" v-if="v$.password.$error">
          {{ v$.password.$errors[0].$message }}
        </span>
      </div>
    </div>
    <br />

    <div class="row g-3 align-items-center">
      <div class="col-auto d-block mx-auto">
        <button type="submit" class="btn btn-primary">Login</button>
        <button
          type="button"
          @click="redirectTo('SignUpPage')"
          class="btn btn-link"
        >
          Sign Up
        </button>
      </div>
    </div>
  </form>
</template>

<script>
import { mapActions } from "vuex";
import useValidate from "@vuelidate/core";
import { required, email, minLength } from "@vuelidate/validators";
import { reactive, computed } from "vue";

export default {
  name: "LoginForm",
  setup() {
    const state = reactive({
      email: "",
      password: "",
    });

    const rules = computed(() => {
      return {
        email: { required, email },
        password: { required, minLength: minLength(6) },
      };
    });

    const v$ = useValidate(rules, state);

    return {
      state,
      v$,
    };
  },
  data() {
    return {};
  },
  methods: {
    ...mapActions(["redirectTo"]),
    onSubmit: function () {
      this.v$
        .$validate()
        .then((data) => {
          console.log(data);
          if (data) {
            console.log(this.state);
          }
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style></style>
