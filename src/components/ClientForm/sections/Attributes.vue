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
    <PhoneInput
      v-model.trim="$v.phone_number.$model"
      label="Номер телефона*"
      name="phone_number"
      :error="$v.phone_number.$error"
    />
    <FormSelector :options="client_groups" label="Группа клиентов*" multiple />
    <FormSelector :options="practitioners" label="Лечащий врач" />
    <div v-if="!$v.name.required && $v.name.$dirty" class="error">
      Field is required
    </div>
  </div>
</template>

<script>
import { required } from "vuelidate/lib/validators";
import FormInput from "../FormInput.vue";
import PhoneInput from "../PhoneInput.vue";
import FormSelector from "../FormSelector.vue";

export default {
  name: "AttributesSection",

  components: {
    FormInput,
    PhoneInput,
    FormSelector,
  },

  data() {
    return {
      surname: "",
      name: "",
      patronymic: "",
      phone_number: "",
      client_groups: ["VIP", "Проблемные", "ОМС"],
      practitioners: ["Иванов", "Захаров", "Чернышева"],
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
    phone_number: {
      required,
    },
  },
};
</script>

<style>
</style>