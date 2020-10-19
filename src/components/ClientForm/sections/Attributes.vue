<template>
  <div class="form-section">
    <FormDatePicker
      v-model="$v.DOB.$model"
      label="Дата рождения*"
      name="DOB"
      :error="$v.DOB.$error && isFormDirty"
    >
      <div v-if="DOBRequiredError">Требуется указать дату рождения.</div>
    </FormDatePicker>
    <FormInput
      v-model.trim="$v.surname.$model"
      label="Фамилия*"
      name="surname"
      :error="$v.surname.$error && isFormDirty"
    >
      <div v-if="surnameRequiredError">Требуется заполнить поле.</div>
      <div v-if="surnameMinLengthError">Минимум 3 символа.</div>
    </FormInput>
    <FormInput
      v-model.trim="$v.name.$model"
      label="Имя*"
      name="name"
      :error="$v.name.$error && isFormDirty"
    >
      <div v-if="nameRequiredError">Требуется заполнить поле.</div>
      <div v-if="nameMinLengthError">Минимум 3 символа.</div>
    </FormInput>
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
      :error="$v.phoneNumber.$error && isFormDirty"
    >
      <div v-if="phoneNumberStartsWithSevenError">
        Номер телефона должен начинаться с цифры "7".
      </div>
      <div v-if="phoneNumberElevenDigitsError">
        Номер телефона должен содержать 11 цифр.
      </div>
    </PhoneInput>
    <FormSelector v-model="selectedGender" :options="genderList" label="Пол" />
    <FormSelector
      v-model="selectedClientGroups"
      :options="clientGroups"
      label="Группа клиентов*"
      multiple
      :error="$v.selectedClientGroups.$error && isFormDirty"
    >
      <div v-if="clientGroupsRequiredError">Нужно выбрать группу.</div>
    </FormSelector>
    <FormSelector
      v-model="selectedPractitioner"
      :options="practitioners"
      label="Лечащий врач"
    />
    <FormCheckbox
      v-model="doNotSendSMS"
      name="doNotSendSMS"
      label="Не отправлять СМС"
    />
  </div>
</template>

<script>
import { required, minLength } from "vuelidate/lib/validators";
import FormInput from "../FormInput.vue";
import PhoneInput from "../PhoneInput.vue";
import FormSelector from "../FormSelector.vue";
import FormCheckbox from "../FormCheckbox.vue";
import FormDatePicker from "../FormDatePicker.vue";

export default {
  name: "AttributesSection",

  components: {
    FormInput,
    PhoneInput,
    FormSelector,
    FormCheckbox,
    FormDatePicker,
  },

  props: {
    isFormDirty: {
      type: Boolean,
      default: false,
    },
  },

  data() {
    return {
      surname: "",
      name: "",
      patronymic: "",
      DOB: "",
      phoneNumber: "",
      genderList: ["Женский", "Мужской"],
      selectedGender: "",
      clientGroups: ["VIP", "Проблемные", "ОМС"],
      selectedClientGroups: [],
      practitioners: ["Иванов", "Захаров", "Чернышева"],
      selectedPractitioner: "",
      doNotSendSMS: false,
    };
  },

  validations: {
    surname: {
      required,
      minLength: minLength(3),
    },
    name: {
      required,
      minLength: minLength(3),
    },
    patronymic: {},
    phoneNumber: {
      required,
      startsWithSeven: (val) => {
        return val.startsWith("7");
      },
      elevenDigits: (val) => {
        return val.length === 11;
      },
    },
    selectedClientGroups: {
      required,
    },
    DOB: {
      required,
    },
  },

  computed: {
    surnameRequiredError() {
      return (
        !this.$v.surname.required && this.$v.surname.$dirty && this.isFormDirty
      );
    },
    surnameMinLengthError() {
      return (
        !this.$v.surname.minLength && this.$v.surname.$dirty && this.isFormDirty
      );
    },
    nameRequiredError() {
      return !this.$v.name.required && this.$v.name.$dirty && this.isFormDirty;
    },
    nameMinLengthError() {
      return !this.$v.name.minLength && this.$v.name.$dirty && this.isFormDirty;
    },
    DOBRequiredError() {
      return !this.$v.DOB.required && this.$v.DOB.$dirty && this.isFormDirty;
    },
    phoneNumberStartsWithSevenError() {
      return (
        !this.$v.phoneNumber.startsWithSeven &&
        this.$v.phoneNumber.$dirty &&
        this.isFormDirty
      );
    },
    phoneNumberElevenDigitsError() {
      return (
        !this.$v.phoneNumber.elevenDigits &&
        this.$v.phoneNumber.$dirty &&
        this.isFormDirty
      );
    },
    clientGroupsRequiredError() {
      return (
        !this.$v.selectedClientGroups.required &&
        this.$v.selectedClientGroups.$dirty &&
        this.isFormDirty
      );
    },
  },

  watch: {
    isFormDirty() {
      this.$v.$touch();
    },
  },
};
</script>

<style lang="scss">
.form-section {
  width: 240px;
}
</style>