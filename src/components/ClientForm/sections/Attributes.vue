<template>
  <div class="form-section">
    <FormInput
      v-model.trim="$v.surname.$model"
      label="Фамилия*"
      name="surname"
      :error="$v.surname.$error"
    />
    <FormInput
      v-model.trim="$v.name.$model"
      label="Имя*"
      name="name"
      :error="$v.name.$error"
    />
    <FormInput
      v-model.trim="$v.patronymic.$model"
      label="Отчество"
      name="patronymic"
      :error="$v.patronymic.$error"
    />
    <div v-if="!$v.name.required && $v.name.$dirty" class="error">
      Field is required
    </div>
  </div>
</template>

<script>
import { required } from "vuelidate/lib/validators";
import FormInput from "../FormInput.vue";

export default {
  name: "AttributesSection",

  components: {
    FormInput,
  },

  data() {
    return {
      surname: "",
      name: "",
      patronymic: "",
    };
  },

  validations: {
    surname: {
      required,
    },
    name: {
      required,
    },
    patronymic: {},
  },
};
</script>

<style>
</style>