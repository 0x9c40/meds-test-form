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
      v-model.trim="$v.phoneNumber.$model"
      label="Номер телефона*"
      name="phoneNumber"
      :error="$v.phoneNumber.$error"
    />
    <FormSelector :options="genderList" label="Пол" />
    <FormSelector
      :options="clientGroups"
      label="Группа клиентов*"
      multiple
      :error="$v.selectedClientGroup.$error"
      @selection="onSelection"
    />
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
      phoneNumber: "",
      genderList: ["Женский", "Мужской"],
      clientGroups: ["VIP", "Проблемные", "ОМС"],
      practitioners: ["Иванов", "Захаров", "Чернышева"],
      selectedClientGroup: [],
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
    phoneNumber: {
      required,
    },
    selectedClientGroup: {
      required,
    },
  },

  methods: {
    onSelection(event) {
      this.selectedClientGroup = event;
      this.$v.selectedClientGroup.$touch();
    },
  },
};
</script>

<style>
</style>