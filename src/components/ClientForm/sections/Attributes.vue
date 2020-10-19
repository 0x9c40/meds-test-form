<template>
  <div class="form-section">
    <FormInput
      v-model.trim="$v.surname.$model"
      label="Фамилия*"
      name="surname"
      :error="$v.surname.$error && toucher"
    >
      <div v-if="surnameRequiredError">Требуется заполнить поле.</div>
      <div v-if="surnameMinLengthError">Минимум 3 символа.</div>
    </FormInput>
    <FormInput
      v-model.trim="$v.name.$model"
      label="Имя*"
      name="name"
      :error="$v.name.$error && toucher"
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
      :error="$v.phoneNumber.$error && toucher"
    >
      <div v-if="phoneNumberStartsWithSevenError">
        Номер телефона должен начинаться с цифры "7".
      </div>
      <div v-if="phoneNumberElevenDigitsError">
        Номер телефона должен содержать 11 цифр.
      </div>
    </PhoneInput>
    <FormSelector :options="genderList" label="Пол" />
    <FormSelector
      :options="clientGroups"
      label="Группа клиентов*"
      multiple
      :error="$v.selectedClientGroup.$error && toucher"
      @selection="onSelection"
    >
      <div v-if="clientGroupsRequiredError">Нужно выбрать группу.</div>
    </FormSelector>
    <FormSelector :options="practitioners" label="Лечащий врач" />
    <!-- v-model="doNotSendSMS" -->
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

export default {
  name: "AttributesSection",

  components: {
    FormInput,
    PhoneInput,
    FormSelector,
    FormCheckbox,
  },

  props: {
    touch: {
      type: Number,
      default: 0,
    },
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
      doNotSendSMS: false,
      toucher: false,
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
    selectedClientGroup: {
      required,
    },
  },

  computed: {
    surnameRequiredError() {
      return (
        !this.$v.surname.required && this.$v.surname.$dirty && this.toucher
      );
    },
    surnameMinLengthError() {
      return (
        !this.$v.surname.minLength && this.$v.surname.$dirty && this.toucher
      );
    },
    nameRequiredError() {
      return !this.$v.name.required && this.$v.name.$dirty && this.toucher;
    },
    nameMinLengthError() {
      return !this.$v.name.minLength && this.$v.name.$dirty && this.toucher;
    },
    phoneNumberStartsWithSevenError() {
      return (
        !this.$v.phoneNumber.startsWithSeven &&
        this.$v.phoneNumber.$dirty &&
        this.toucher
      );
    },
    phoneNumberElevenDigitsError() {
      return (
        !this.$v.phoneNumber.elevenDigits &&
        this.$v.phoneNumber.$dirty &&
        this.toucher
      );
    },
    clientGroupsRequiredError() {
      return (
        !this.$v.selectedClientGroup.required &&
        this.$v.selectedClientGroup.$dirty &&
        this.toucher
      );
    },
  },

  watch: {
    touch() {
      this.toucher = true;
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

<style lang="scss">
.form-section {
  width: 240px;
}
</style>